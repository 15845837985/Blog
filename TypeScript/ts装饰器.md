# 装饰器：

装饰器是一种特殊类型的声明，它能够被附加到类声明、方法、属性或参数上，可以修改类的行为。

通俗来说，装饰器就是一个方法，可以注入到类、方法、属性、参数上来扩展类、方法、属性、参数的功能。

常见的装饰器有：类装饰器、方法装饰器、属性装饰器、参数装饰器

装饰器的写法：普通装饰器（无法传参）、装饰器工厂（可传参）

装饰器是过去几年中js最大成就之一，已是ES7的标准特性之一

## 类装饰器：

类装饰器在声明之前被声明（紧靠着类声明）。类装饰器应用于类构造函数，可以在不更改类的定义的情况下动态地监视，修改或替换类定义。传入一个参数

### 普通装饰器：

```
function logClass(params:any){
    console.log(params);
    params.prototype.apiUrl = 'xxxxx';
    params.prototype.run = function(){
        console.log('run');

    }
}

@logClass
class HttpClient{
    constructor(){

    }
    getData(){

    }
}

var http:any = new HttpClient();
console.log(http.apiUrl);
http.run();
```

### 装饰器工厂：

```
function logClass(params:string){
    return function(target:any){
        console.log(target);

        console.log(params);

        target.prototype.apiUrl = params;

    }
}

@logClass('hahaha')
class HttpClient{
    constructor(){

    }
    getData(){

    }
}

var http:any = new HttpClient();
console.log(http.apiUrl);
```

例子：

重载构造函数

类装饰器表达式会在运行时当作函数被调用，类的构造函数作为其唯一标识符

如果类装饰器返回一个值，它会使用提供的构造函数来替换类的声明

```
function logClass(target:any){
    console.log(target);
   return class extends target{
       apiUrl:any = '我是修改后的apiUrl';
       getData(){
           console.log(this.apiUrl + '(已变更)');

       }
   }
}

@logClass
class HttpClient{
    public apiUrl:string | undefined;
    constructor(){
        this.apiUrl = '我是构造函数中的apiUrl'
    }
    getData(){
        console.log(this.apiUrl);

    }
}
```

## 属性装饰器：

属性装饰器表达式会在运行时当作函数被调用，需要传入两个参数

1.对于静态成员来说是类的构造函数，对于实例成员是类的原型对象

2.成员的名字

```
function logClass(params:string){
    return function(tarfet:any){

    }
}
function logProperty(params:any){
    return function(target:any,attr:any){
        console.log(target);
        console.log(attr);
        target[attr] = params /* target在这里相当于target.prototype*/
    }
}


@logClass('xxx')
class HttpClient{
    @logProperty('aaaaaa')
    public url:any | undefined;
    constructor(){

    }
    getData(){
        console.log(this.url);

    }
}

var http = new HttpClient();
http.getData();
```

## 方法装饰器：

会被应用到方法的属性描述符上，可以用来监视，修改或者替换方法定义。

需要传入三个参数：

1.对于静态成员来说是类的构造函数，对于实例成员是类的原型对象

2.成员的名字

3.成员的属性描述符

```
function get(params:any) {
    console.log(params) // 装饰器传入的参数：http://baidu.com
    return function(target:any, methodName:any, desc:any) {
        console.log(target)  // { constructor:f, getData:f } 
        console.log(methodName)  // getData
        console.log(desc)  // {value: ƒ, writable: true, enumerable: false, configurable: true} value就是方法体
        /* 修改被装饰的方法 */
        //1. 保存原方法体
        var oldMethod = desc.value;
        //2. 重新定义方法体
        desc.value = function(...args:any[]) {
            //3. 把传入的数组元素都转为字符串
            let newArgs = args.map((item)=>{
                return String(item);
            });
            //4. 执行原来的方法体
            oldMethod.apply(this, newArgs);
            // 等效于 oldMethod.call(this, ...newArgs);
        }
    }
}
class HttpClient {
    constructor() { }
    @get('http://baidu.com')
    getData(...args:any[]) {
        console.log('getData: ', args);
    }
}
var http = new HttpClient();
http.getData(1, 2, true);  // getData: ["1", "2", "true"]
```

tip:

在我自己写这个例子的时候遇到了问题，如果使用ts-node在ts环境下执行可以看到成员属性描述符的内容，如果在js环境下运行成员属性描述符则为undefined，我在网上搜索了一下并没有发现相同问题，开始我怀疑是我编译器的问题，我的编译器一直没有办法以管理员的权限运行终端，可是我以管理员身份在命令提示符中运行时也存在一样的问题，只有使用ts-node命令在ts环境下运行时可以正常显示属性描述符。欢迎了解原因的大佬给我指点迷津。

## 方法参数装饰器：

参数装饰器表达式会在运行时被调用，可以为类的原型增加一些元素数据，传入3个参数：

1. 对于静态成员来说是类的构造函数，对于实例成员来说是类的原型对象
2. **方法名称**，如果装饰的是构造函数的参数，则值为`undefined`
3. 参数在函数参数列表中的索引；

```
function logParams(params:any) {
    console.log(params)  // 装饰器传入的参数：uuid
    return function(target:any, methodName:any, paramIndex:any) {
        console.log(target)  // { constructor:f, getData:f } 
        console.log(methodName)  // getData
        console.log(paramIndex)  // 0
    }
}
class HttpClient {
    constructor() { }
    getData(@logParams('uuid') uuid:any) {
        console.log(uuid);
    }
}
```

注意：

* 参数装饰器只能用来监视一个方法的参数是否被传入；
* 参数装饰器在`Angular`中被广泛使用,特别是结合`reflect-metadata`库来支持实验性的`Metadata API`
* 参数装饰器的返回值会被忽略。

## 装饰器的执行顺序：

装饰器组合：TS支持多个装饰器同时装饰到一个声明上，语法支持从左到右，或从上到下书写；

```
@f @g x

@f
@g
x
```

在TypeScript里，当多个装饰器应用在一个声明上时会进行如下步骤的操作：

1. 由上至下依次对装饰器表达式求值;
2. 求值的结果会被当作函数，由下至上依次调用.

不同装饰器的执行顺序：属性装饰器 &gt;方法装饰器 &gt;参数装饰器 &gt;类装饰器

```
function logClz11(params:string) {
    return function(target:any) {
        console.log('logClz11')
    }
}
function logClz22(params?:string) {
    return function(target:any) {
        console.log('logClz22')
    }
}
function logAttr(params?:string) {
    return function(target:any, attrName:any) {
        console.log('logAttr')
    }
}
function logMethod(params?:string) {
    return function(target:any, methodName:any, desc:any) {
        console.log('logMethod')
    }
}
function logParam11(params?:any) {
    return function(target:any, methodName:any, paramIndex:any) {
        console.log('logParam11')
    }
}
function logParam22(params?:any) {
    return function(target:any, methodName:any, paramIndex:any) {
        console.log('logParam22')
    }
}

@logClz11('http://baidu.com')
@logClz22()
class HttpClient {
    @logAttr()
    public url:string|undefined;

    constructor() { }

    @logMethod()
    getData() {
        console.log('get data');
    }

    setData(@logParam11() param1:any, @logParam22() param2:any) {
        console.log('set data');
    }
}
// logAttr --> logMethod --> logParam22 --> logParam11 --> logClz22 --> logClz11
```



