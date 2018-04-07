---
title: JS标准库和数组
date: 2018-03-27 12:21:19
tags:
---
## 1. String
```
String(s);    //'s'，不加new 就直接输出字符串
new String(s)    //String{'s'}，加new就输出一个对象
```

## 2. Number
```
Number(sss)    //报错，Error: sss is not defined
Number('sss')    //NaN，NaN也是一个数字
Number(1)    //1
Number('1')    //1
new Number(123)    //Number{123}，加new就变成对象
```

## 3. Boolean
```
6个falsy值
Boolean(false)    //false
Boolean(undefined)    //false
Boolean(null)    //false
Boolean(NaN)    //false
Boolean('')    //false
Boolean(0)    //false

其他的全是true
```
## 4. 基本类型和复杂类型的区别
![数据类型.png](/images/数据类型.png)

除了对象（包括数组、函数）是复杂类型，其他数据类型都是基础类型

## 5. Object
```
Object(1);    //Number{1}，前加new 和不加new是一样的
Object('s')    //String{'s'}
Object()    //{}
```

## 6. Array
**1. 用法**
    第一种用法：
    ```
    let a = ['a','b'];    //['a','b']
    let b = new Array('a','b');   //['a','b']
    //上面两种写法效果是一样的

    let a = Array(3)  //创建了一个长度为3的空数组
    a.length    //3
    a[0]    //undefined
    0 in a    //false

    let a = new Array(3)     //和上面一样
    ```
    第二种用法：
    ```
    let a = Array(3,3);    //[3,3]，length为2
    //这和第一种一样的写法，功能却不同，不一致性，JS的垃圾之处
    ```
**2. 什么是数组？**![数组.png](/images/数组.png)数组就是对象，是拥有特殊原型链的对象,有Array.prototype的就是数组，没有的就不是数组
**3. 伪数组**
```
let obj = {
    0:'1',
    1:'2',
    length:2;
} //看起来像数组，但没有Array.prototype的，就是伪数组
```
   arguments是伪数组

**4. 数组的API**
  1. forEach
```
var a = ['a','b','c'];
a.forEach(function(x,y){
  console.log(y);    //y是key
  console.log(x);    //x是value
})
//0 a
//1 b
//2 c
```

  2. sort，这个API会改变原值！**只有这一个API会改变原值**
```
var l = [2,3,1];
     
l.sort();    //[1,2,3]，从小到大排序
l.sort(function(a,b){return a-b}) //[1,2,3]，从小到大排序    
l.sort(function(a,b){return b-a}) //[3,2,1]，从大到小排序    

//按成绩高到低排名
var students = ['小明','小红','小花'];
var scores = { 小明: 59, 小红: 99, 小花: 80 };
students.sort(function(x,y){return scores[y] - scores[x]})    // ["小红", "小花", "小明"]
```
3. join
```
var a = [1,2,3];
    
a.join('方方');    //'1方方2方方3'
a.join();    //'1,2,3'，默认是逗号
```
4. concat
```
var a = [1,2,3];
var b = [3,4,5];
var c = a.concat(b);    //'1,2,3,3,4,5'

var d = a.concat([]);    //'1,2,3'，d和a的值一样，但d和a是两个数组，所以concat可以用来深拷贝数组
```
5. map（映射）
```
var a = [1,2,3];
a.map(function(value,key){
  return value * 2;
})    //[2,4,6];
a.map(value => value * 2);    //[2,4,6]
```
6. filter（过滤器）
```
var a = [1,2,3,4,5];
a.filter(function(value,key){
   return value >= 3;
})    //[3,4,5]
a.filter(function(value,key){
    return value % 2 === 0 ;
})    //返回偶数，[2,4]

a.filter(function(value,key){
  return value % 2 === 0 ;
}).map(function(value){
    return value * value;
})     //[4,16];
```
7. reduce
```
var a = [1,2,3];
a.reduce(function(sum,n){
   return sum + n ;
},0)    //6，求和，0是初始值，第一次传给sum的就是0，sum是每次传进来的值，之后传给sum的是return里的值，n是遍历的数
    
a.reduce((sum,n) => sum + n ,0)    //6，箭头函数的写法
```
map可以用reduce表示：
```
a.reduce(function(arr,n){
    arr.push(n*2);
    return arr;
},[])    //[2,4,6]
```
filter也可以用reduce表示：
```
a.reduce(function(arr,n){
  if(n % 2 === 0){
      arr.push(n)
}
  return arr;
},[])
```
只要掌握reduce就行了
8. splice
```
array.splice(start)
array.splice(start, deleteCount) 
array.splice(开始的位置, 删除的个数, 插入的对象1,插入的对象2, ...)
```
9. slice
```
array.slice()  //保留完整数组
array.slice(4)  //保留4到最后的数组
array.slice(4,8)  //保留4到8以前的数组
```