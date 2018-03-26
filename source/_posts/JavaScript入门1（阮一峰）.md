---
title: JavaScript入门1（阮一峰）
date: 2018-03-21 13:50:03
tags:
---
# 1. 语法
```
1. div1 = document.createElement('div')   //要加引号
2. div.textContent = '我是div'
3. main.appendChild(div1)  //这个不用引号
4. key.className = 'key'
```

# 2. 包装函数
当用js创建一个span标签并想同时给它添加className和textContent时，可以用一个函数来一起实现，如：
```
function createSpan(textContent) {
    var span = tag('span',{className:'text',textContent:textContent});
    return span;
}

var span  = createSpan('sb'); // 这样可以直接创建className为text、textContent为sb的span标签
```

# 3. 用canvas的时候获取用户页面宽高的API
```
var pageWidth = document.documentElement.clientWidth;
var pageHeight = document.documentElement.clientHeight;

canvas.width = pageWidth
canvas.height = pageHeight
```

# 4. 数据类型（背下来）
##### 1. 数值(number)
> var a = 011        // a === 9，**0开头代表8进制！**
var b = 0b11         // b === 3，0b开头代表2进制
var c = 0x11         // c === 17，0x代表16进制

##### 2. 字符串(string)
> JavaScript 认为'𝌆'的长度为2，而不是1。
对于码点在U+10000到U+10FFFF之间的字符，JavaScript 总是认为它们是两个字符（length属性为2）。所以处理的时候，必须把这一点考虑在内，也就是说，JavaScript 返回的字符串长度可能是不正确的。
##### 3. 布尔值(boolean)
##### 4. symbol
> 用来生成一个全局唯一的值
##### 5. undefined   6. null
>null和undefined都表示没有值，一般来说
1.若一个变量没有赋值，例：var a;，则a的值就是undefined
2.若创建一个对象，现在还不想赋值，则可以var obj = null;
3.若一个number、string不想赋值，则可以参照第一条

##### 7. 对象(object)
前面六种是简单类型或基本类型，对象是合成类型
对象可以分成：
           > 狭义的对象
           > 数组
           > 函数   

> 当你在遍历对象的时候
> ```
> var person = {name:'pyz',age:18}
>for(var key in person){
>   console.log(person[key]); >//console.log(person.key);
>}
> ```
>用person.key和person[key]是不同的，person.key代表person里有一个键名为key的属性，key被当作字符串，会出现undefined。而且数值键名也不能用点，会被当作小数点。
`obj.123    //报错`
只能用person[key]来表示，因为使用方括号运算符时key会被当作变量来处理。

> bug1: typeof null     //object
bug2: typeof function      //function，function也是object的一种，但function有自己的原型
 
>{foo:123}，javascript理解为语句（即代码块）
({foo:123})，JavaScript理解为对象
在eval语句（作用是对字符串求值）中
eval('{foo: 123}') // 123
eval('({foo: 123})') // {foo: 123}

>一般遍历对象自身属性时结合使用hasOwnProperty方法
>```
>var person = { name: '老彭' };
>for (var key in person) {
>  if (person.hasOwnProperty(key)) {
>    console.log(key);
>  }
>}
>// name
>```
>查看一个对象本身的所有属性，也可以使用Object.keys方法
>```
>var obj = {
>  key1: 1,
>  key2: 2
>};
>
>Object.keys(obj);
>// ['key1', 'key2']
>```


# 5. 数值
1. JavaScript里不要直接比较小数，因为浮点数不是精确的值
```
0.1 + 0.2 === 0.3
// false

0.3 / 0.1
// 2.9999999999999996

(0.3 - 0.2) === (0.2 - 0.1)
// false
```
2. JavaScript 对15位的十进制整数都可以精确处理，大于15位就不行了

3. 以下两种情况，JavaScript 会自动将数值转为科学计数法表示
（1）小数点前的数字多于21位。
（2）小数点后的零多于5个。

4. JavaScript 对整数提供四种进制的表示方法：十进制、十六进制、八进制、二进制。默认情况下，JavaScript 内部会自动将八进制、十六进制、二进制转为十进制。
 > 十进制：没有前导0的数值。
八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。
十六进制：有前缀0x或0X的数值。
二进制：有前缀0b或0B的数值。

# 6. 字符串
若字符串要换行的话，可以这样
```
'a\
b\
c'
//‘abc’
```
**重点是\后只能加回车，不能有任何空格**