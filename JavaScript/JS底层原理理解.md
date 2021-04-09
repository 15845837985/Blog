### 变量：

变量对象 \(缩写为VO\)就是与执行上下文相关的对象，与代数一样，JavaScript 变量可用于存放值（比如 x=5）和表达式（比如 z=x+y）。

变量可以使用短名称（比如 x 和 y），也可以使用描述性更好的名称（比如 age, sum, totalvolume）。

* 变量必须以字母开头
* 变量也能以 $ 和 \_ 符号开头（不过我们不推荐这么做）
* 变量名称对大小写敏感（y 和 Y 是不同的变量）

说到变量就不得不提JS中的数据类型

### 数据类型：

JS中的数据类型分为基本数据类型和引用数据类型

基本数据类型包括：number string boolean null undefined symbol\(ES6\) 按值访问，可以操作保存在变量中实际的值。

引用数据类型为Object（array，function，date...） 引用类型的值是保存在内存中的对象。

### 类型转换：

1.typeof:

```
typeof 1 // 'number' 
typeof '1' // 'string' 
typeof undefined // 'undefined' 
typeof true // 'boolean' 
typeof Symbol() // 'symbol' 
typeof b // b 没有声明，但是还会显示 undefined 
typeof [] // 'object' 
typeof {} // 'object 
typeof null // 'object' 
typeof console.log // 'function'
```

PS：instanceof也可以判断对象类型，因为内部机制通过判断对象的原型链中是不是能找到类型的prototype

2.valueOf:

对象在转换基本类型时，首先会调用 valueOf 然后调用 toString。并且这两个方法是可以重写的。

```js
let a = { 
           valueOf() { 
               return 0 
            },
            toString() { 
                return 'a'; 
            }, 
        } 
console.log(a); // {value:f, toString:f}
console.log(a.toString()); // a
console.log(a + 1); // 1
console.log('a' + 1); // a1
console.log(a + '1'); //01
```

每个对象都有一个toString\(\)方法和value方法，其中toString\(\)方法返回一个表示该对象的字符串，value方法返回该对象的原始值。对于toString方法来说，当对象被表示为文本值或者当以期望字符串的方式引用对象时。该方法被自动调用。对于一个对象，toSting\(\)返回"\[object type\]",其中type是对象类型。如果x不是对象，toString\(\)返回应有的文本值。

对于valueOf\(\) 方法来说，默认情况下, valueOf\(\) 会被每个对象Object继承。每一个内置对象都会覆盖这个方法为了返回一个合理的值，如果对象没有原始值，valueOf\(\) 就会返回对象自身。

```js
let a = { 
           valueOf() { 
               return 0 
            },
            toString() { 
                return 'a'; 
            }, 
            [Symbol.toPrimitive]() { 
                return 2; 
            } //优先级最高
        } 
console.log(a); // {value:f, toString:f, Symbol(Symbol.toPrimitive):f}
console.log(a.toString()); // a
console.log(a + 1); // 3
console.log('a' + 1); // a1
console.log(a + '1'); //21
```

对象的Symbol.toPrimitive属性。指向一个方法。该对象被转化为原始类型的值时，会调用这个办法，返回该对象对应的原始类型值。  
Symbol.toPrimitive被调用时,会接受一个字符串参数，表示当前运算的模式，一个有三种模式。

* Number:该场合需要转成数值
* String:该场合需要转成字符串
* Default:该场合可以转成数值，也可以转成字符串。

PS:关于valueOf\(\),toString\(\),Symbol.toPrimitive详细用法及区别可以参考：[https://segmentfault.com/a/1190000016300245](https://segmentfault.com/a/1190000016300245)

3.比较运算符：

如果是对象，就通过toPrimitive转换对象

如果是字符串，就通过unicode字符索引来比较

```js
let a = {
    [Symbol.toPrimitive](hint) {
        if (hint === 'number') {
                return 42;
        }
        return null;
    }
};
let b = {
    [Symbol.toPrimitive](hint) {
        if (hint === 'number') {
                return 23;
        }
        return null;
    }
};
let str1 = 'aaa';
let str2 = 'bbb'
console.log(a > b); //true
console.log(str1 < str2); //false
```

PS:两个无Symbol.toPrimitive属性的空对象没有可比性，建议补充查看一下js中各种数据类型的存储位置

还有一个小例子：比较0.1+0.2!=0.3 而0.2+0.3=0.5

记住，永远不要直接比较俩个浮点的大小。这个属于数字运算中的精度缺失的问题在0.1 + 0.2这个式子中，0.1和0.2都是近似表示的，在他们相加的时候，两个近似值进行了计算，导致最后得到的值是0.30000000000000004，此时对于JS来说，其不够近似于0.3，于是就出现了0.1 + 0.2 != 0.3 这个现象。 当然，也并非所有的近似值相加都得不到正确的结果。有时两个近似值进行计算的时候，得到的值是在JS的近似范围内的，于是就可以得到正确答案。至于哪些值计算后能得到正确结果，哪些不能，我们也不需要去记。最好的方法就是我们想办法规避掉这类小数计算时的精度问题就好了，那么最常用的方法就是将浮点数转化成整数计算。因为整数都是可以精确表示的。

4.四则运算：

只有当加法运算时，其中一方是字符串类型，就会把另一个也转为字符串类型。

其他运算只要其中一方是数字，那么另一方就转为数字。

并且加法运算会触发三种类型转换：将值转换为原始值，转换为数字，转换为字符串。

```
1 + '1' // '11' 
2 * '2' // 4 
[1, 2] + [2, 1] // '1,22,1' 
// [1, 2].toString() -> '1,2' 
// [2, 1].toString() -> '2,1' 
// '1,2' + '2,1' = '1,22,1' 
// 对于加号需要注意这个表达式 
'a' + + 'b' 'a' + + 'b' // -> "aNaN" 
// 因为 + 'b' -> NaN
```

PS: NaN 属于 number 类型，并且 NaN 不等于自身。

undefined 不是保留字，能够在低版本浏览器被赋值 let undefined = 1

### 实例对象：

1.new:

在调用 new 的过程中会发生以上四件事情

新生成一个对象 ----&gt; 链接到原型 ----&gt; 绑定this ----&gt; 返回新对象

```js
// ES5构造函数
let Parent = function (name, age) {
    this.name = name;
    this.age = age;
};
Parent.prototype.sayName = function () {
    console.log(this.name);
};
const child = new Parent('听风是风', 26);
child.sayName() //'听风是风'


//ES6 class类
class Parent {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    sayName() {
        console.log(this.name);
    }
};
const child = new Parent('echo', 26);
child.sayName() //echo

function myNew() { 
        // 创建一个空的对象 
        let obj = new Object() 
        // 获得构造函数 
        let Con = [].shift.call(arguments) 
        // 链接到原型 
        obj.__proto__ = Con.prototype 
        // 绑定 this，执行构造函数 
        let result = Con.apply(obj, arguments) 
        // 确保 new 出来的是个对象 
        return typeof result === 'object' ? result : obj 
}
```

2.new中执行的优先级：

```js
 function Foo() {
    return this;
}
Foo.getName = function () {
    console.log('1');
};
Foo.prototype.getName = function () {
    console.log('2');
};

new Foo.getName();   // -> 1
new Foo().getName(); // -> 2

// new Foo() 的优先级大于 new Foo

// new (Foo.getName()); //1
(new Foo()).getName(); //2

// 对于第一个函数来说，先执行了 Foo.getName() ，所以结果为 1；
// 对于后者来说，先执行 new Foo() 产生了一个实例，
// 然后通过原型链找到了 Foo 上的 getName 函数，所以结果为 2。
```

3.this:

通用规则new有最高的优先级，可以通过call，apply，bind改变this，优先级仅次于new。

```

```

箭头函数没有this，箭头函数中的的this取决于他外面的第一个不是箭头函数的函数的this

### 执行上下文：

全局执行上下文

函数执行上下文

eval 执行上下文

1.属性 VO & AO：

变量对象 \(缩写为VO\)就是与执行上下文相关的对象，它存储下列内容：

1. 变量 \(var, VariableDeclaration\);
2. 函数声明 \(FunctionDeclaration, 缩写为FD\);
3. 函数的形参

4. 只有全局上下文的变量对象允许通过VO的属性名称间接访问\(因为在全局上下文里，全局对象自身就是一个VO\(稍后会详细介绍\)。在其它上下文中是不可能直接访问到VO的，因为变量对象完全是实现机制内部的事情。当我们声明一个变量或一个函数的时候，同时还用变量的名称和值，在VO里创建了一个新的属性。

激活对象是函数上下文里的激活对象AO中的内部对象，它包括下列属性：

1. callee — 指向当前函数的引用；
2. length —真正传递的参数的个数；
3. properties-indexes\(字符串类型的整数\)

4. 属性的值就是函数的参数值\(按参数列表从左到右排列\)。 properties-indexes内部元素的个数等于arguments.length. properties-indexes 的值和实际传递进来的参数之间是共享的。\(译者注：共享与不共享的区别可以对比理解为引用传递与值传递的区别\)

2.属性this & 作用域链

```js
b(); // call b
console.log(a); //undefined

var a = 'hello world';
function b(){
    console.log('call b')
}
```

以上众所周知因为函数和变量提升的原因。通常提升的解释是说将声明的代码移动到了顶部。但是更准确的解释应该是：在生成执行上下文时，会有两个阶段。第一个阶段是创建的阶段（具体步骤是创建 VO），JS解释器会找出需要提升的变量和函数，并且给他们提前在内存中开辟好空间，函数的话会将整个函数存入内存中，变量只声明并且赋值为 undefined，所以在第二个阶段，也就是代码执行阶段，我们可以直接提前使用。

在提升的过程中，相同的函数会覆盖上一个函数，并且函数优先于变量提升

### 深浅拷贝：

1.浅拷贝

通过Object.assign

```js
let a = {
    age:1
};
let b = Object.assign({},a);
a.age = 2;
console.log(b.age); // 1
```

通过展开运算符

```js
let a = {
    age:1
};
let b = {...a};
a.age = 2;
console.log(b.age); // 1
```

浅拷贝的弊端：浅拷贝只解决了第一层的问题，如果接下去的值中还有对象的话，那么两者享有相同的引用。要解决这个问题需要引入深拷贝。

2.深拷贝

通过JSONparse\(JSON.stringify\(object\)\)

```js
let a = {
    age:1'
    jobe:{
        first:'FE'
    }
};
let b = JSON.parse(JSON.stringify(a));
a.jobs.first = 'native';
console.log(b.jobs.first) // FE
```

该方法会忽略undefined，忽略函数，不能解决循环引用的对象，若数据中包含上述三种情况，可以通过lodash的深拷贝函数或者使用MessageChannel

```js
function structuralClone(obj) {
    return new Promise(resolve => {
        const {port1,port2} = nwe MessageChannel();
        port2.onmessage = ev => resolve(ev.data);
        port1.postMessage(obj);
    });
}
var obj = {
    a:1,
    b:{
        c:b
    }
}
//该方法是异步的
//可以处理 undefined和循环引用对象
const clone = await structuralClone(obj);
```

### JavaScript运行机制及原理：

#### 事件执行

1. 单线程，同一个时间只能做一件事
2. 任务分为同步和异步，于是运行机制可以简单理解成一个主线程（执行栈）和一个任务队列，主线程运行完成之后，再从任务队列中读取事件运行。这个过程循环不断，又称Event Loop

#### 变量/函数的预解析

1. JavaScript会对基础类型的变量进行预解析（变量提升），对函数声明（不包括函数）进行预加载。
2. 对于变量的定义，无论是否存在逻辑判断，JavaScript都会进行预解析，而对于函数声明，JavaScript并不会对逻辑判断中的进行预加载，只会对函数主体中暴露的进行预加载。

```
console.log(a,b,c);
var b = 'b';
if(true){
    var a = 'a';
}
if(false){
    var c = 'c';
}
console.log(a,b,c);
//输出结果
undefined undefined undefined
a b undefined


faz('faz');
//foo('foo');
//bar('bar');
if(true){
    function foo(x){
        console.log(x);
    }
}
if(false){
    function bar(x){
        console.log(x);
    }
}
function faz(x){
    console.log(x);
}
foo('foo');
bar('bar');
//输出结果
faz
foo
Uncaught TypeError: bar is not a function
```

#### JavaScript 预加载顺序

1. 首先会对所有声明前置（变量提升）
2. 函数的参数，如果有参数直接赋值

   3.函数内部的函数声明，如果有则前置，如果函数名与参数重复则覆盖掉参数

3. 函数内部的变量声明，如果有则前置，如果变量名与 函数声明重复 会忽略该变量声明，只是忽略声明 赋值语句仍有效

```
!function(x,y){
    alert(x); //function
    alert(y); //2
    var x = 10,y=20;
    function x(){}
    alert(x); //10
    alert(y);  //20
}(2,2)
```

#### 闭包/作用域 call apply bind

1. 如果一个函数调用了函数作用域外的一个变量，那么这个函数和变量就统称为闭包    闭包的作用：1.希望一个变量长期驻扎在内存中，2.避免全局污染，3.可以在循环中找到对应元素的索引 不需要再添加索引
2. call和apply方法类似，区别就是call\(\)方法接受的是参数列表，apply\(\)方法接受的是一个参数数组。bind\(\)方法与call\(\)类似，但是是创建一个新的函数。call和apply方法都是立即调用，而bind方法需要手动调用。

```
var m = {
    "x" : 1
};
function foo(y) {
    console.log(this.x + y);
}
foo(5);
foo.apply(m, [5]);
foo.call(m, 5);
var foo1 = foo.bind(m, 5);
foo1();
//输出结果
NaN
6
6
6
```

#### JavaScript 原型理解

1. undefined，null，boolean，string，number五种基本类型，一种复杂类型object。
2. String，Array，Boolean，Object都可以理解为构造函数，而JavaScript中Function 类型有一个属性 prototype，直接翻译过来就是原型。这个属性就是一个指针，指向一个对象，这个对象包含一些属性和方法，这些属性和方法会被当前函数生成的所有实例（对象）所共享。普通对象有个不规范的“原型”对象，在chrome和Firefox中以 
   **proto**
   表示，本文暂时称为隐式原型。 每个函数对象都有一个 prototype 对象，即为原型。原型也有隐式原型指向Object的原型即Object.prototype。而函数对象本身的隐式原型则都指向Function.prototype。
3. 重要公式  
   `var 对象 = new 函数() 对象.__proto__ === 对象的构造函数.protoytpe`

   推导：

```
var number = new Number()
number.__proto__ = Number.prototype
Number.__proto__ = Function.prototype // 因为 Number 是 Function 的实例

var object = new Object()
object.__proto__ = Object.prototype
Object.__proto__ = Function.prototype // 因为 Object 是 Function 的实例

var function = new Function()
function.__proto__ = Function.prototype
Function.__proto__ == Function.prototye // 因为 Function 是 Function 的实例！
Function.prototye.__proto__ = Object.prototype//Function.prototye是个对象
```



