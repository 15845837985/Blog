# 第一章 TypeScript基础:

## TypeScript环境安装：

安装：

1. 首先需要安装node.js以及npm（npm会随着node.js一同安装），安装方法在node.js官网下载并且一路下一步即可，不在此赘述
2. 全局安装TypeScript： npm install -g typescript
3. 校验TypeScript: tsc -v \(显示出版本号，即ts已安装成功\)

tsc作用：负责将ts代码转换为浏览器、nodejs识别的js代码

xxx.ts文件无法直接在浏览器中运行，需要使用tsc工具（使用方法：tsc  ts文件名）将ts代码编译为js代码后由浏览器或者nodejs执行js代码

推荐一个工具：ts-node

可以使用ts-node将ts代码转化为js代码，并直接在nodejs中执行

安装：npm install -g ts-node

使用：ts-node ts文件名

## TypeScript数据类型：

### typescript变量声明：

TypeScript语法规定：在声明变量的时候，必须要指定变量的类型。

声明变量的语法：

let 变量名：变量类型；

let age: number;

let name: string;

变量类型一旦指定后，这个变量中只能存储这个类型的数据。

```
let age: number;
age = 10;
// age = "zhangsan" 报错，不能将age赋值为字符串
```

### TypeScript数据类型：

TypeScript兼容JavScript的所有数据类型：string、 number、 boolean、 null、 undefined、 Symbol

除此之外还包括数组类型（array）、元组类型（tuple）、枚举类型（enum）、任意类型（any）、void类型、never类型...

### array：

```
let arr1:number[] = [1,2,3,4];
let arr2:Array<number> = [11,22,33]
```

### tuple：

```
let arr:[string,number,boolean] = ["ts",1,true]
```

##### 元组属于数组的一种

### enum：

在其他程序设计语言中，一般用一个数值来代表一种状态，这种方法不直观，易读性差。如果能在程序中用自然语言中有相应含义的单词来表达某一状态，则程序就会容易阅读和理解。也就是说，是先考虑某一变量可能的取值，并尽量用自然语言中的含义解释每一个值，这种方法称为枚举法，用这种方法定义的类型称为枚举类型

定义方式：

enum 枚举名{

```
标识符\[=整型常数\]，

标识符\[=整型常数\]，

...

标识符\[=整型常数\]，
```

};

```
enum Flag {
success=1, 
error=-1
};
let f:Flag=Flag.success
console.log(f); //输出1
```

```
enum Color {red,blue=5,orange}
var a:Color=Color.red;
var b:Color=Color.blue;
var c:Color=Color.orange;
console.log(a); //未赋值输出索引值
console.log(b); //输出5
console.log(c); //输出6， 根据最近的已赋值元素计算
```

### undefined与null：

JavScript中                                                                        TypeScript中

undefined：代表变量未初始化                                         undefined：代表变量只能存储undefined类型的值

null：代表变量指向一个空对象                                        null：代表变量只能存储null值

##### tip：因为undefined和null为其他类型的子类，所以这两个变量的值可以赋值给其他类型的变量

```
let age: number;
age = 10;
// age = "zhangsan" 报错，不能将age赋值为字符串
age = null;

let a1: undefined = undefined;
// a1 = 10;   报错
let a2: null = null;
// a2 = "null"   报错
```

### 联合类型：

let 变量名： 数据类型1 \| 数据类型2 \|  ...；      变量的值可以是几种类型中的任意一种

```
let result: string | number;
result = 1;
console.log("resulet = " + result);
result = "zhangsan"
console.log("resulet = " + result);
// result = true
```

### any:

any类型的变量，可以存储任意类型的数据

```
let v1: any;
v1 = 1;
v1 = "lisi";
v1 = true;
v1 = [10, 20, 30];
v1 = {
    name: "lisi",
    age: 1
}
```

## TypeScript函数：



