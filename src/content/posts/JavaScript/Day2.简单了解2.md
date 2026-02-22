---
title: Day2.简单了解2
published: 2026-02-21
description: ''
image: ''
tags: [JavaScript]
category: 'JavaScript'
draft: false
lang: ''
---
## 对象数组和JSON
对象数组和JSON格式上相似，有如下区别：


JSON是一种轻量级的数据交换格式，而对象数组是一种在JavaScript中常用的数据结构。
JSON是一种文本格式，而对象数组是一种JavaScript对象。
JSON只能表示简单的数据类型（如字符串、数字、布尔值、数组和对象），而对象数组可以表示更复杂的数据类型（如函数、日期、正则表达式等）。
JSON数据必须是双引号括起来的字符串，而对象数组可以使用单引号或双引号括起来的字符串。
JSON数据只能表示键值对，而对象数组可以包含任意数量的属性。
JSON数据只能表示简单的结构，而对象数组可以表示更复杂的结构（如嵌套数组和对象）。

```javascript
let todos = [
    {
        id: 1,
        title: "学习HTML",
        completed: true

    },
    {
        id: 2,
        title: "学习CSS",
        completed: false
    },
    {
        id: 3,
        title: "学习JavaScript",
        completed: false
    }
]
console.log(todos)
console.log(todos[2].title)
  
  
//转化
const todoJSON = JSON.stringify(todos)
console.log(todoJSON)

//再转回去
const JSON1 =  '[{"id":1,"title":"title1","completed":true},{"id":2,"title":"学习CSS","completed":false},{"id":3,"title":"学习JavaScript","completed":false}]'
const todoObj = JSON.parse(JSON1)
console.log(todoObj)
```

输出结果：
```
[
  { id: 1, title: '学习HTML', completed: true },
  { id: 2, title: '学习CSS', completed: false },
  { id: 3, title: '学习JavaScript', completed: false }
]
学习JavaScript
[{"id":1,"title":"学习HTML","completed":true},{"id":2,"title":"学习CSS","completed":false},{"id":3,"title":"学习JavaScript","completed":false}]
[
  { id: 1, title: 'title1', completed: true },
  { id: 2, title: '学习CSS', completed: false },
  { id: 3, title: '学习JavaScript', completed: false }
]
```

## if，一些运算符，switch语句，for循环,while循环
```javascript
const a = 10

if (a == 10) {
    console.log("a等于10")
}
//=== 严格等于，不仅要值相等，还要类型相等
if (a === 10) {
    console.log("a等于10")
}

if (a === "10") {
    console.log("a等于\"10\"")
} else if (a > 10) {
    console.log("a大于10")
} else {
    console.log("a不等于\"10\"")
}
// ||表示或        &&表示和
//与c++类似
  

//三目运算符 也与c++类似
const b = a>10?"a大于10":"a不大于10"
console.log(b)
  

//switch 用法仍然与c++类似
//若不加break，则会继续执行后续所有case
const c = red
switch (c) {
    case "red":
        console.log("c等于red")
        break;
    case "green":
        console.log("c等于green")
        break;
    default:
        console.log("c不等于red或green")
        break;
}
```

循环：
```javascript
//仍然与c++类似
for(let i = 0;i<5;i++){
    console.log(i)
}

let i = 0
while(i<5){
    console.log(i)
    i++
}

//中括号数组大括号对象
let todos = [
    {
        id: 1,
        title: "学习HTML",
        completed: true
    },
    {
        id: 2,
        title: "学习CSS",
        completed: false
    },
    {
        id: 3,
        title: "学习JavaScript",
        completed: false
    }
]
for(let i = 0;i<todos.length;i++){
    console.log(todos[i].title)
}
//或者
for (let todo of todos){
    console.log(todo.title)
}
```
输出结果：
```
0
1
2
3
4
0
1
2
3
4
学习HTML
学习CSS
学习JavaScript
学习HTML
学习CSS
学习JavaScript
```

简单了解就到这里，接下来会是更加深入的学习