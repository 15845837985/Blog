# js常用API

## Array：

1.concat\(\)：连接两个或多个数组，返回一个新数组 ，参数可以是具体的值也可以是数组对象，**返回数组 不改变原数组**

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
var arr2 = new Array(3);
  arr2[0] = "Kobe";
  arr2[1] = "Gaso";
  arr2[2] = "Fisher";
var arr3 = arr1.concat(arr2);
  alert(arr1.concat(arr1,arr2);
```

2.join\(\)：把数组中的所有元素放入一个字符串，元素通过指定分隔符分隔，返回一个字符串，参数为分隔符，省略参数则默认使用逗号作为分隔符 **返回字符串 不改变原数组**

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
var arr2 = new Array(3);
  arr2[0] = "Kobe";
  arr2[1] = "Gaso";
  arr2[2] = "Fisher";
var arr3 = arr1.concat(arr2);
  alert(arr1.join("."));
```

3.pop\(\)：删除数组的最后一个元素，把数组长度减1，并**返回删除的元素的值**如果数组以为空，则pop\(\)不改变数组，并返回undefined

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
alert(arr1.pop());
doucument.write(arr);
```

4.push\(\)：把参数顺序添加到数组的尾部  **修改数组**，并**返回新的长度**

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
aler(arr1.push("Shardo"))
doucument.write(arr);
```

Tip:结合push\(\)方法和pop\(\)方法我们便可以用数组模拟栈的数据结构（先进后出）

5.reverse\(\)：颠倒数组中元素的顺序  **修改数组 返回数组**

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
doucument.write(arr1);
```

6.unshift\(\): 将参数添加到原数组开头并**返回数组长度** ** 改变原数组**

```
var arr = [1,2,3,4,5];
arr.push(6,7,8,9);
console.log(arr.unshift("01","02","00"));
console.log(arr);        
```

6.shift\(\)：把数组的第一个元素删除  **修改数组**，并**返回第一个元素的值**（数组原来的第一个元素，即被删除的元素），如果数组是空的，那么shift方法不进行任何操作，返回undefined

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
aler(arr1.shift())
doucument.write(arr1);
```

7.slice\(\)：从已有数组中返回选定的元素（**不会修改数组只是返回一个子数组**），参数（start，end），其中start必填规定从何处开始选取。如果是负数则从数组尾部开始算起，即-1为最后一个元素，-2为倒数第二个元素以此类推。end为可选参数，规定从何处结束选取，如果没有指定该参数那么切分的数组包含从start到数组结束的所有元素，如果是负数，规定的是从数组尾部开始算起的元素。

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
alert(arr1.slice(1));
document.write(arr1 + "<br />");
var arr2 = new Array(6);
  arr2[0] = "Kobe";
  arr2[1] = "James";
  arr2[2] = "Davis";
  arr2[3] = "Gaso";
  arr2[4] = "Kuzma";
  arr2[5] = "Fisher";
alert(arr2.slice(2,4));
document.write(arr2);
```

8.sort\(\)：对数组元素进行排序，参数可选规定排序顺序，必须是函数，没有参数时按照字母编码顺序进行排序，如果打算按照其他准则进行排序就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明两个值相对顺序的数字，比较函数应具有两个参数a和b，若a小于b，在排序后的数组中a在b前，返回一个小于0的值，若a等于b，则返回0，若a大于b则返回一个大于0的值。**返回值为对数组的引用，数组在原数组上进行排序，不生成新副本**

```
var arr2 = new Array(6);
        arr2[0] = "Kobe";
        arr2[1] = "James";
        arr2[2] = "Davis";
        arr2[3] = "Gaso";
        arr2[4] = "Kuzma";
        arr2[5] = "Fisher";
document.write(arr2.sort() + "<br />");
function sortNum(a,b) {
   return a - b  //升序为a-b，降序为b-a
};
var arr3 = new Array(6);
        arr3[0] = "10";
        arr3[1] = "5";
        arr3[2] = "40";
        arr3[3] = "25";
        arr3[4] = "1000";
        arr3[5] = "1";
document.write(arr3.sort(sortNum) + "<br />");
```

9.splice\(\)：向/从数组中添加/删除，然后返回被删除的项目（**会改变原始数组**），arrayObject.splice\(index,howmany,item1,....,itemX\)，参数中index：为规定添加/删除项目的位置，使用负数可以从数组结尾处规定位置（必须，整数），howmany：需要删除的项目数量（必填，若为0则不删除），item1,...,itemX：向数组添加新的项目（可选）**返回数组 改变原数组**

```
var arr2 = new Array(6);
    arr2[0] = "Kobe";
    arr2[1] = "James";
    arr2[2] = "Davis";
    arr2[3] = "Gaso";
    arr2[4] = "Kuzma";
    arr2[5] = "Fisher";
    arr2.splice(2,0,"Willian")
document.write(arr2 + "<br />");
```

10.includes\(\)判断数组是否包含某项，**返回布尔值 **不利用严格等于判断，可以判断是否是NaN

```
[1,2,3,4,5].includes(4) //true
```

## ES6中新方法：

1.from\(\),将类数组（类似数组的对象，本质上具有length属性都可以使用Array.from\(\)转为数组）和可遍历对象（ES6中的set、map数据结构）转换为数组 **返回数组**

```
let myArr = {'0':'a','1':'b','2':'c'};
let arr = Array.from(myArr);
console.log(arr); //[] 无length属性

let myArr2 = {'0':'a','1':'b','2':'c'，length=3};
let arr2 = Array.from(myArr2);
console.log(arr2); //['a','b','c'] 

console.log(Array.from({length=2})); //[undefined,undefined]
```

* 若参数是一个数组Array.from\(\)会返回一个一样的新数组
* Array.from\(\)可以接受第二个参数用来对每一个元素处理并放入返回的数组中
* Array.from\(\)可以将字符串转化为

```
let myArr = {0:1,1:2,2:3，length：3};
let arr = Array.from(myArr，x => x*x);
console.log(arr); //[ 1, 4, 9 ]

function countSymbols(string){
    return Array.from(string).length;
}
```

2.of\(\),将一组值转化为数组 **返回数组  **可以用来弥补数组构造函数Array的不足，在构造函数中如果只有一个值，那么这个值认作为数组长度而非数组的第一个值

```
console.log(Array.of(1,2,3));  //[1,2,3]
console.log(Array.of(undefined));  //[undefined]
console.log(Array.of());  // [] 无参时返回空数组
```

## JS中常见的循环遍历：

1.array.map\(\):**返回一个数组**，数组中的元素为原数组元素调用处理函数后的值 **不可使用break/continue跳出循环**

```
var numbers = [1,2,3,4];
var num1 = numbers.map(value => value * 2);
console.log(num1); //[2,4,6,8]
```

2.array.some\(\),**返回布尔值**，用于检测数组中是否满足函数提供的指定条件，some\(\)会依次执行数组中的每一个元素，有一个满足条件即返回true，随即跳出循环，剩余元素不会再执行检测，如果没有满足的条件则返回false  **return true时跳出循环**

```
var w = ['a','b','c','d','e'];
var show = [];
w.some((item,index) => {
    if(index === 2){
        return true
    }
    show.push(item)
})
    console.log(show); //['a','b']
```

3.array.every\(\),**返回布尔值**，检测数组中是否每一项都满足条件 **return false时跳出循环**

```
var w = ['a','b','c','d','e'];
var show = [];
w.every((item,index) => {
    if(index === 2){
        return false
    }
    show.push(item)
    return item
})
    console.log(show);  //['a','b']  这里输出了a和b 是因为在every中return了内容，否则在every中的第一次检测时会因为return false直接跳出循环
```

4.forEach\(\),对数组进行循环遍历，对数组中每一项运行给定函数，参数为function默认有传参，参数分别为遍历的数组内容、对应数组索引、数组本身， **无返回值 不可使用break/continue跳出循环**

```
 nameList = ["James","Curry","Durant"];
 nameList.forEach((item,index,array) => {
     console.log(item + "---" + index);
 })
```

5.fliter\(\),创建一个新数组，其中元素是指定数组中符合条件的所有元素 **不会检测空数组 返回数组 不会改变原数组 不可以使用break/continue跳出循环**

```
var ages = [3,6,18,20];
var m1 = ages.filter(item => item >= 18);
console.log(ages);
console.log(m1);
```



