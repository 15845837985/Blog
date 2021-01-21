# **前言介绍：**

TypeScript是由微软开发的一款开源的编程语言。TypeScript是JavaScript的超集，包含ES5、ES6。同时，也新增加了一些语法，比如关于类型和面向对象的语法。TypeScript更像后端Java、C\#这样的面向对象语言，可以让js开发大型企业项目。最新的Vue、Ract也可以集成TypeScript。

这部分内容中会包含一些ES5、ES6中的使用方法以及TypeScript中的使用方法以供对比参照。

### TypeScript环境安装：

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

