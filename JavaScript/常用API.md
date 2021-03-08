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



