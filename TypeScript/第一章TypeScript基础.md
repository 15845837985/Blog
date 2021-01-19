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

## TypeScript函数：



