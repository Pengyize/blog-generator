---
title: JavaScript原型
date: 2018-03-23 12:47:25
tags:
---
## 1. 公用属性（就是原型）
每个对象都有toString()、valueof()等方法，但他们并其实没有单独的方法，而是JS在每个对象里都存了一个隐藏属性：\_\_proto__，这个属性指向了存放公用属性（原型）的地址，当用toString()时，就是调用的公用属性（原型）
```
o1.toString === o2.toString   //true
```
同时Number对象还有它特有的公用属性（原型），所以它比Object要多一个公用属性库，并且会先访问Number的原型（公用属性库），**这一条链就叫原型链**，像下图![原型链](/images/原型链.png)
同理，String、boolean也有自己的原型，但若平常没被引用的话会被当作垃圾回收，所以平常对象的原型是Object.prototype在引用，可得⬇️
```
Object.prototype === o1.__proto__     //true，是把prototype的地址赋给__proto__属性了
```
所以它们最终指向的Object的公有属性，就是Object.prototype（原型），Number特有的公有属性就是Number.prototype，同理有
```
Number.prototype.__proto__ === Object.prototype //true，是把Object.prototype的地址赋给Number的__proto__属性了

var n1 = new Number(1);
n1.__proto__ === Number.prototype    //true，是把Number.prototype的地址赋给n1的__proto__属性了
n1.__proto__.__proto__ === Object.prototype  //true
```

## 2. \_\_proto\_\_和prototype的区别
![原型.png](/images/原型.png)
打开浏览器就会自动生成Number、String、Boolean、Object这几个对象和它们的原型，并把它们原型的地址放入prototype属性里，在你写：
```
var n = new Number(1);     //就会把Number.prototype里的地址放入n的__proto__属性里
```
这样用n就能调用Number的原型了

总结：
```
var 对象 = new 函数();
对象.__proto__ === 函数.prototype    //true
```
\_\_proto\_\_是对象的属性，prototype是函数的属性
**面试题**：`'1'.__proto__`是什么？
答：'1'会临时转化为String对象，'1'.\_\_proto\_\_指向String.prototype

所有对象都有\_\_proto\_\_属性
```
Object.prototype.\_\_proto\_\_ === null;

1.toString()     //语法错误，JS把.当作小数点了
1..toString()    //'1'，第一个.当作小数点，第二个为点操作符
```