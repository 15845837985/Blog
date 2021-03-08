# js常用API

## Array：

1.concat\(\)：连接两个或多个数组，返回一个新数组 ，参数可以是具体的值也可以是数组对象

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

2.join\(\)：把数组中的所有元素放入一个字符串，元素通过指定分隔符分隔，返回一个字符串，参数为分隔符，省略参数则默认使用逗号作为分隔符

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

3.pop\(\)：删除数组的最后一个元素，把数组长度减1，并返回删除的元素的值如果数组以为空，则pop\(\)不改变数组，并返回undefined

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
alert(arr1.pop());
doucument.write(arr);
```

4.push\(\)：把参数顺序添加到数组的尾部（**push\(\)会修改数组**），并返回新的长度

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
aler(arr1.push("Shardo"))
doucument.write(arr);
```

Tip:结合push\(\)方法和pop\(\)方法我们便可以用数组模拟栈的数据结构（先进后出）

5.reverse\(\)：颠倒数组中元素的顺序（**reverse\(\)会修改数组**）

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
doucument.write(arr1);
```

6.shift\(\)：把数组的第一个元素删除（shift\(\)会修改数组），并返回第一个元素的值（数组原来的第一个元素，即被删除的元素），如果数组是空的，那么shift方法不进行任何操作，返回undefined

```
var arr1 = new Array(3);
  arr1[0] = "James";
  arr1[1] = "Davis";
  arr1[2] = "Kuzma";
aler(arr1.shift())
doucument.write(arr1);
```

7.slice\(\)：从已有数组中返回选定的元素（不会修改数组只是返回一个子数组），参数（start，end），其中start必填规定从何处开始选取。如果是负数则从数组尾部开始算起，即-1为最后一个元素，-2为倒数第二个元素以此类推。end为可选参数，规定从何处结束选取，如果没有指定该参数那么切分的数组包含从start到数组结束的所有元素，如果是负数，规定的是从数组尾部开始算起的元素。

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

8.sort\(\)：对数组元素进行排序，参数可选规定排序顺序，必须是函数，没有参数时按照字母编码顺序进行排序，如果打算按照其他准则进行排序就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明两个值相对顺序的数字，比较函数应具有两个参数a和b，若a小于b，在排序后的数组中a在b前，返回一个小于0的值，若a等于b，则返回0，若a大于b则返回一个大于0的值。返回值为对数组的引用，数组在原数组上进行排序，不生成新副本

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

9.splice\(\)：向/从数组中添加/删除，然后返回被删除的项目（**会改变原始数组**），arrayObject.splice\(index,howmany,item1,....,itemX\)，参数中index：为规定添加/删除项目的位置，使用负数可以从数组结尾处规定位置（必须，整数），howmany：需要删除的项目数量（必填，若为0则不删除），item1,...,itemX：向数组添加新的项目（可选）

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



