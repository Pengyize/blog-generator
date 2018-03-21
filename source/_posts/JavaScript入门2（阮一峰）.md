---
title: JavaScript入门2（阮一峰）
date: 2018-03-21 14:12:42
tags:
---
## 1. 数组
数组本身是对象，是一种特殊的对象
#### 1.length
数组不能用点结构读取
```
var a = [1,2];
a[0]        //        1
a.0         //        SyntaxError: Unexpected number
a.length    //        2，数组默认有length值

a[9] = 10;
a.length    //        10，JavaScript还是会认为长度是10，会把中间的值都当作empty
```
JavaScript用32位整数保存数组的长度，所以数组最多只能有2^32^-1个，数组length的值是可以设置的，a.length = 0可以用来清空数组。
```
var a = [1,2,3];
a.length = 0;
a        //        []
```
人为设置是多少数组的长度就是多少，若length大于原来的值，多出来的叫空位，读取空位会返回undefined，用in运算符会返回false。
```
var a = [1,2,3];
a.length = 10
a[5]    //    undefined

2 in a  // true
3 in a  // false
```
将数组的键分别设为字符串和小数，结果都不影响length的值，所以length只和数字键有关。
```
var a = [];

a['p'] = 'abc';
a.length           //    0
a[2.1] = 'abc';
a.length           //    0
```


如果数组的键名是添加超出范围的数值，该键名会自动转为字符串。
```
a[-1] = 'a';
a[Math.pow(2, 32)] = 'b';

a.length // 0
a[-1] // "a"
a[4294967296] // "b"
```

#### 2. in
```
var arr = [ 'a', 'b', 'c' ];
2 in arr  // true
'2' in arr // true
4 in arr // false ，不存在就是false

arr[100] = 'a';
100 in arr // true
99 in arr // false，空位也会被认为是false
```
#### 3. 遍历数组
```
var colors = ['red', 'green', 'blue'];
colors.forEach(function (color) {
  console.log(color);
});
```
用length遍历数组时，会把空位输出为undefined，但使用数组的forEach方法、for...in结构、以及Object.keys方法进行遍历，空位都会被跳过，只有当数组的值是undefined时，它们才会输出undefined
```
var a = [ ,2,3];

for(var i=0;i<a.length;i++){
    console.log(a[i]);            //undefined   2   3
}

a.forEach(function (x, i) {
    console.log(i + ':' + x);     // 1:2   2:3
});

a = [undefined,2,3];

a.forEach(function (x, i) {
    console.log(i + ':' + x);     // 0:undefined   1:2   2:3
});
```
#### 4. delete
```
var a = [1, 2, 3];
delete a[1];

a[1] // undefined
a.length // 3
```
delete不会影响length，所以用length遍历数组的时候要小心

#### 5.类似数组的对象
可以把类似数组对象转为真正的数组，详情见[阮一峰-数组-类似数组的对象](http://javascript.ruanyifeng.com/grammar/array.html)

#### 6. 
```
typeof [1,2,3];      //      'object'  注意返回字符串
```
