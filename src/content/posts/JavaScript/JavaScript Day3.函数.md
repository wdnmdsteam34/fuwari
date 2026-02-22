---
title: JavaScript Day3.函数
published: 2026-02-22
description: ''
image: ''
tags: [JavaScript]
category: 'JavaScript'
draft: false
lang: ''
---
# 函数
## 箭头函数

### 传统显性写法
```javascript
function add(a, b) {
  return a + b;
}
a = 10
b = 20
console.log(add(a, b))
//与c++类似
```
### 隐性写法（匿名函数）
#### 传统匿名函数写法
```javascript
const add = function(a,b){
	return a+b;
}
```
#### 箭头函数写法
```javascript
const add = (a,b) => {
	return a+b;
}
//箭头函数省字
//当箭头函数只有一个参数时，可以省略小括号，0个以及>=2个都不行
//当箭头函数只有一条语句时，可以省略花括号和return关键字，但若保留花括号且有输出值，则return不能省。保留return关键字则花括号不能省
const double = a => a*2;
```
#### 立即执行函数（IIFE
也是一种匿名函数，用法是立即执行函数表达式的内容，可以防止变量污染。
如果代码前面有其他语句，建议在 IIFE 前面加上分号，避免与上一行连接导致错误
```javascript
(function(){console.log(10)})()//第一个括号是把函数声明（function（）是一个函数声明）转化为函数表达式，第二个括号是执行这个函数表达式
;(()=> console.log(11))()
```

函数还有函数提升的性质：无论函数在何处声明，都默认在文件开头加载。不会出现C++中需要把函数提前的情况。但是只有标准的具名函数（显性函数）才有这个特征。用let/const定义的以及立即执行函数都不具备这个特征。
```javascript
// ✅ 函数声明 - 可以提升
sayHi();
function sayHi() { console.log("Hi"); }

// ❌ 函数表达式 - 相当于 let，不能提升
sayHello();
let sayHello = function() { console.log("Hello"); };
// 报错：sayHello is not a function
```
####  另外介绍一些数组高阶函数

| 名       | 作用                                   |
| ------- | ------------------------------------ |
| map     | 遍历数组每个元素进行一定操作后返回新的数组                |
| filter  | 遍历数组每个元素进行一定判断后返回判断结果为true的原元素值组成的数组 |
| find    | 找到第一个符合要求的元素                         |
| forEach | 只是相当于一个for循环遍历的简化写法                  |

```javascript
const aa = [1,2,3,4,5]
console.log(aa.map(function(c,b) {return c*b}))//普通匿名函数必须有大括号和return
console.log(aa.map((c,b) => c*b))//箭头函数可以省略return关键字
console.log(aa.filter((c,b) => c*b%3==0))//只返回下标和值的乘积为3的倍数的原元素值
console.log(aa.find(a => a>2))//返回第一个大于2的元素值
console.log(aa.forEach((x,y) => console.log(`第${y}个元素是${x}`)))//只遍历，不返回值，因此foreach外层的console.log会输出一个undefined

```
返回结果：
```javascript
[ 0, 2, 6, 12, 20 ]
[ 0, 2, 6, 12, 20 ]
[ 1, 3, 4 ]
3
第0个元素是1
第1个元素是2
第2个元素是3
第3个元素是4
第4个元素是5
undefined
```
## 回调函数

把函数当参数用
调用某个函数时，函数也可以作为参数传入。
```javascript
//回调函数 不需要自己经常写回调函数，但会用到很多别人写好的回调（比如 fetch、数组方法等）
const bb = 1
const callback = () => console.log("回调函数调用了")
const function1 = (bb,callback) => {//只是参数，要在
    console.log(bb);
    callback()
}
function1(bb,callback)
```
# 异步
## setTimeout
先执行后面的同步任务，同步任务执行完后再通过等待时间大小决定同层异步之间的先后顺序。
```javascript
console.log(1);
setTimeout(()=>{
    console.log(2);
})
console.log(3);
```

输出：

```javascript
1
3
2
```
更复杂一点：
```javascript
console.log(1);
setTimeout(()=>{
    console.log(2);
    setTimeout(()=>{
        console.log(3);
    })
    console.log(4);
},11)
setTimeout(()=>{
    console.log(5);
},1)
console.log(6);
```
输出：
```javascript
1
6
5
2
4
3
```
是不是看着很乱？可读性非常差。为了解决这个问题，promise应运而生。
## 了解promise

```javascript
// 创建promise的方法
//依旧了解，不是让你写的，是让你知道有这么个东西
const p1 = new Promise((成功,失败)=>{
//这里可以写成功或失败，作为函数名，后面跟的参数传到then/catch里
//成功和失败都写一遍只会管第一个（这里是成功
 成功("请求成功")//这时候p1的内容就是  Promise { '请求成功' }
 失败("请求失败")//若把成功注释/本行提前则运行.catch的结果
})
//.then或.catch后面跟的括号里是一个参数，这个参数是函数，函数会被分配一个默认参数，这个参数是promise返回的内容。
p1.then(结果=>{console.log(结果)})
.catch(结果=>console.log(结果))
function aaa(a){console.log(a)}
p1.then(aaa)//这里函数aaa不用写括号给参数，因为.then直接把参数传给aaa了
```
返回结果：
```javascript
请求成功
请求成功
```
另外：
```javascript
p1 = new Promise((成功, 失败) => {
    失败("请求异常")
})
p1.then(成功的结果 => {
    console.log(成功的结果)
    return Promise.resolve("下一个then的参数")
},失败的结果=>{
    console.log(失败的结果)
    // return Promise.reject()
    // 或者抛出异常
    throw new Error("请求失败")//有第二个参数时不会调用.catch，因此实战中不建议写第二个参数。并且错误处理是异步的，因此会先调用下面的输出1
}
)
.catch(结果=>{
    console.log(结果);
})
console.log("1")
```
输出：
```javascript
1
请求异常
Error: 请求失败
    at C:\ESD\js学习\ls.js:11:11
```
## 用promise简化回调地狱

```javascript
setTimeout(() => {
    console.log("s加载第一项");
    setTimeout(() => {
        console.log("s加载第二项");
        setTimeout(() => {
            console.log("s加载第三项");
            setTimeout(() => {
                console.log("s加载第四项");
            }, 1000);
        }, 1000);
    }, 1000);
}, 1000);
//改为：
Promise.resolve()
.then(()=>{
    console.log("p加载第一项");
    return Promise.resolve()
})
.then(()=>{
    console.log("p加载第二项");
    return Promise.resolve()  
})
.then(()=>{
    console.log("p加载第三项");
    return Promise.resolve()
})
.then(()=>{
    console.log("p加载第四项");
})
//代码长度先不管，你就说是不是好看多了吧
//从文字提示可以看出来，一般用在需要按顺序执行的异步操作上
//比如：加载数据后渲染页面，每个步骤都依赖前一个步骤的结果
```
结果：
```javascript
p加载第一项
p加载第二项
p加载第三项
p加载第四项
s加载第一项
s加载第二项
s加载第三项
s加载第四项
```
## Async
	可以看出，promise仍然有些臃肿，因此Async横空出世！
	