---
title: ES6入门
date: 2018-04-13 21:10:20
tags:
---
# 1. let语法，用法和var一样
### 1. 作用域不同
若用let来声明变量，只在let命令所在的代码块内有效。而var只有在function内用才能有块级作用域效果，除了function，在其他地方用var全声明的是全局变量
```
//例1
{
  let a = 10;
  var b = 1;
}
a // ReferenceError: a is not defined.
b // 1

//例2
for (let i = 0; i < 3; i++) {
  let i = 'abc';  //这个i和上面的数字i不互相影响
  console.log(i);
}
// abc
// abc
// abc
```
### 2. let不会变量提升！

# 2. 解构赋值
```
let method = options.method;
let body = options.body;
let successFn = options.successFn 

//下面是es6，下面这一行相当于上面三行
let {method,body,successFn} = options; 
```
若是用在函数里：
```
function(options){
  let {method,body,successFn} = options;
}

//上面这样可以简化为下面

function({method,body,successFn}){
  //直接把这个当参数，省略options
}
```