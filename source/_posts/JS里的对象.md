---
title: JS里的对象
date: 2018-03-23 12:44:48
tags:
---
## 1. 全局变量:一种是 ECMAScript 规定的（global）

- global.parseInt
- global.parseFloat
- global.Number
- global.String
- global.Boolean
- global.Object

## 2. 全局变量:另一种是浏览器自己的全局变量(window)

- window.alert
- window.prompt
- window.comfirm
- window.console.log

## 3. Number
JavaScript的作者Brendan Eich被公司要求JS要像Java，所以他模仿java写了
`var n = new Number(1);`这样n是一个对象，有自己的属性，但太麻烦，于是他又写了一种
`var n =1;`n是基本类型
但他用了一个方法，使这样声明的也可以用Number对象的属性
```
var n=1;
n.toString();       //n用toString时，本质是下面这两行，实质n是没有属性的

var temp = new Number(n);    //声明了一个临时变量temp，并将n作为Number对象赋给它
temp.toString();             //用temp来执行toString，执行完后temp就被抹杀了

n.xxx = 2;      //可以的
n.xxx           //但undefined，因为xxx是存在temp的，上一句的temp执行完后就被抹杀，所以xxx也被抹杀了
```

## 4. String

```
var s = 'asd';      //     原理和Number一样

var s2 = new String(s);
s2[0]    //    'a'，因为String()对象有hash的属性

s[0]     //    'a'，s也能调用这个属性，但s实质没有属性，这个原理和上面Number一样

s.charCodeAt(0)    //    97，a的unicode码
s.charCodeAt(0).toString(16)  //'61'，a的unicode码的十六进制

' asd '.trim();      //  'asd'，去掉字符串两边的空格

var s1 = 'Hello';
s.concat(s1);      //    asdHello，连接两个字符串

s1.slice(0,1);      //   'H'，slice是切片，切下0到1之前的内容
s1.slice(1);        //   'ello'，返回1和后面的所有内容

s1.replace('e','o')    // 'Hollo'，替换

s1.length    //    5

s1.indexOf('o')       //    4，定位，若没找到会返回-1
if(s1.indexOf('h') !== -1) {  // 可用来执行某些操作
  // do stuff with the string
}

s1.toLowerCase();      //    全变成小写
s1.toUpperCase();      //    全变成大写
```

## 5. Boolean
6个falsy值，0、NaN、null、undefined、false、""，除了这6个，其他值都是true
**所有对象都是true**
```
var b = false;
var b1 = new Boolean(false);
if(b){console.log('true')};
if(b1){console.log('true')};      // true
//只会输出b1，因为所有对象都是true！！
```

## 6. Object
```
var o1 = {};      //常用方法
var o2 = new Object();

o1 === o2  //false，因为比较的是地址，而地址不同
```