---
title: Day1
published: 2026-02-20
description: ''
image: ''
tags: ["JavaScript"]
category: 'JavaScript'
draft: false 
lang: ''
---
# Day 1 了解篇
## 1 变量与常量
变量可以用var(不常用),let创建，常量用const创建

**基本用法**
```javascript
var a = 10;//定义a=10
ler b = 20;//定义b=20
const pi = 3.14159;//定义pi=3.14159
```

**var和let的区别：**
```javascript
function test() {
  if (true) {
    var a = 10;
    let b = 20;
  }
  console.log(a); // 10（var 在函数内都有效）
  console.log(b); // 报错：b is not defined（let 只在大括号内有效）
}
test();
```
不用了解太多，无脑用let就行

## 数据类型
### 原生数据类型
包括 `String,Number,Boolean,null,undefined`

| 名称        | 含义               |
| --------- | ---------------- |
| String    | 字符串              |
| Number    | 数字（包括整数和小数       |
| Boolean   | 布尔类型，即 `是` 或 `否` |
| null      | 空类型              |
| undefined | 未定义              |

**undefined与null的区别：**
null是一个确定的类型，undefined就是未定义，包括类型。

**如何查看？**
```javascript
let a = 10.1;
console.log(typeof a);
//输出number
let x = null;
console.log(typeof x);
//输出object
/*
	解释来源于DeepSeek：在 JavaScript 的最初实现中，值在底层存储时会用一个**类型标签**来表示其类型。对象的类型标签是 `0`，而 `null` 在内存中表示为空指针（大多数平台下空指针的值是 `0`）。因此，当 `typeof` 检查类型时，遇到了 `null` 的 `0` 标签，就错误地将其判断为 `"object"`。
*/
```
#### 模板字符串
用来拼接输出的字符串

```javascript
const username = "noname";
const age = "114514";

  

//老方法：
console.log("My name is" + username + "and I am " + age);
//新方法：模板字符串。注意要用反引号。英文标点输入模式下的  ~
console.log(`My name is ${username} and I am ${age}`);
const context = `My name is ${username} and I am ${age}`
console.log(context);
```
输出：
```
My name isnonameand I am 114514
My name is noname and I am 114514
My name is noname and I am 114514
```
#### 一些字符串常用属性和方法
属性没有括号，方法有括号

|属性/方法名     |  作用   | 隶属|
| --- | --- | --- |
|   length  |   输出字符串的长度  |属性|
| toUpperCase | 大写字母 |方法|
| toLowerCase | 小写字母 | 方法 |
| substring | 截取字符串 | 方法 |
| split | 分割字符串 | 方法 |

示例：
```javascript
const a = "Hello World!"

console.log(a.length)
console.log(a.toUpperCase())
console.log(a.toLowerCase())
console.log(a.substring(0,5))//从索引0到索引5

//也可以叠加调用，不同顺序有不同含义，即使结果相同
console.log(a.substring(0,5).toUpperCase())//先截取再大写
console.log(a.toUpperCase().substring(0,5))//先大写再截取
  

//分割字符串成数组
console.log(a.split(""))//最小分割
console.log(a.split("o"))//以'o'为分割点分割，并不会保留'o'
const b = "你 好 世 界"
console.log(b.split(" "))//以空格为分割点分割
```
输出结果：
```
12
HELLO WORLD!
hello world!
Hello
HELLO
HELLO
[
  'H', 'e', 'l', 'l',
  'o', ' ', 'W', 'o',
  'r', 'l', 'd', '!'
]
[ 'Hell', ' W', 'rld!' ]
[ '你', '好', '世', '界' ]
```

### 引用数据类型

|  名称   |   含义  |
| --- | --- |
|    array数组 |  包含多个数据的集合   |
| object对象 | 复合数据类型，用于存储多个相关的属性和方法 |

数组以及一些方法示例：

```javascript
const numbers = new Array(1,2,3,4,5)
console.log(numbers)
console.log(numbers.length)
  

const fruits = ["Apple","Banana","Orange",10,true]
console.log(fruits)
console.log(fruits.length)
fruits[2] = "Peach"//const声明的数组可以改变内部（包括长度和内容）但不能全部改变。
console.log(fruits)
fruits.push("Grape")//在数组末尾添加元素
console.log(fruits)
fruits.pop()//删除数组末尾元素
console.log(fruits)  
fruits.unshift("Watermelon")//在数组开头添加元素
console.log(fruits)
fruits.shift()//删除数组开头元素
console.log(fruits)
fruits.splice(2,1)//删除从索引2开始的1个元素
console.log(fruits)
fruits.splice(2,0,"Lemon")//在索引2处添加元素
console.log(fruits)
/*
array.splice(start, deleteCount, item1, item2, ...)
splice() 方法可以用来删除、添加或替换数组中的元素。
它的第一个参数是要操作的索引位置，第二个参数是要删除的元素数量。
后续的参数是要添加到数组中的元素。
*/


console.log(Array.isArray(fruits))//判断是否为数组
console.log(fruits.indexOf("Banana"))//返回元素首次出现的索引，若不存在则返回-1
console.log(fruits.lastIndexOf("peach"))//返回元素最后一次出现的索引，若不存在则返回-1



/*对于  ‘const声明的数组可以改变内部（包括长度和内容）但不能全部改变。’  的解释：
const 声明的是变量绑定（reference），不是变量值（value）：
const 保证的是：变量名不能重新指向新的内存地址
但原来的内存地址中的内容是可以修改的
*/

/*
fruits = []
修改了数组的指向，不可用。
直接对数组进行赋值是修改其指向。
*/
```

输出：
```
[ 1, 2, 3, 4, 5 ]
5
[ 'Apple', 'Banana', 'Orange', 10, true ]
5
[ 'Apple', 'Banana', 'Peach', 10, true ]
[ 'Apple', 'Banana', 'Peach', 10, true, 'Grape' ]
[ 'Apple', 'Banana', 'Peach', 10, true ]
[ 'Watermelon', 'Apple', 'Banana', 'Peach', 10, true ]
[ 'Apple', 'Banana', 'Peach', 10, true ]
[ 'Apple', 'Banana', 10, true ]
[ 'Apple', 'Banana', 'Lemon', 10, true ]
true
1
-1
```
第一天就学到这里