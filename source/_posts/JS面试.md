---
title: JS面试
date: 2018-05-05 21:51:07
tags:
---
# 1. 数据类型
- number
- string
- boolean
- symbol
- null
- undefine
- object

# 2. promise怎么用
- 生成promise
```
function(){
  return new Promise(function(resolve,reject){
    if(成功){
      resolve()
    }else{
      reject()
    }
  })
}
```
- then
```
$.ajax(...).then(成功函数,失败函数)
```
- then是链式的
```
$.ajax(...).then(成功函数1,失败函数1).then(成功函数2,失败函数2)
//ajax返回404，失败函数1执行，成功函数2执行
```

# 3. 手写ajax
```
let request = new XMLHttpRequest();
request.open('POST','/xxx');
request.onreadystatechange = ()=>{
  if(request.readyState === 4 && request.status === 200){
    var string = request.responseText;
    var value = JSON.parse(string);
  }
}
request.send('a=1&b=2');
```

# 4. 手写闭包
```
function createAdder(){
  let n=1;
  return function(){
    n+=1;
  }
}

let adder = createAdder();
adder()  //n===2
adder()  //n===3
console.log(n)  //n is nor defined
```

# 5. this是什么
1. fn()里面的this正常模式下是Window
2. fn()里面的this严格模式下是undefined
3. a.b.c.fn()里面的this就是a.b.c
4. new F()里面的this就是F()对象
5. () => {console.log(this)}里面的this就是外面的this

# 6. 立即执行函数
`!function(){}()`
作用是创造一个函数作用域，防止污染全局变量
**es6新语法可以代替立即执行函数**
```
{
  let name = 'p'  //用let声明变量即可
}
```

# 7. async/await语法
举例：
```
function returnPromise(){
  return new Promise(function(resolve,reject){
    setTimeout(()=>{
      resolve('参数1')
    },1000)
  })
}

returnPromise().then((result)=>{
   //这个result === '参数1'
})

let result = await returnPromise();
//这个result === '参数1'
```
await可以把异步代码变成同步代码，若Promise运行结果是reject，可用try()catch捕捉到。
加个await就可以等当前异步代码执行完再执行下面的内容
```
function 煮面(){
  水=加水() 
  if(面===false){  
    面 = 去超市买面() //异步操作
  }
  阳春面 = 开火(水，面)
  吃面(阳春面)
}
//这样的结果你只能喝白开水
//但是加上await 就不同了

async function 煮面(){
  水=加水()
  if(面===false){ 
    面 = await 去超市买面() //异步操作
  }
  阳春面 = 开火(水，面)
  吃面(阳春面)
}
//用了await 就可以等面回来以后再执行以下语句
```

# 8. 深拷贝
1. 用JSON深拷贝
```
let a = {...}
let b = JSON.parse(JSON.stringify(a))
```
但这个方法不支持函数、引用、undefined、正则...
2. 递归拷贝
```
var china = {
  nation : '中国',
  birthplaces:['北京','上海','广州'],
  skincolr :'yellow',
  friends:['sk','ls']
}
//深复制，要想达到深复制就需要用递归
function deepCopy(o,c){
  var c = c || {}
  for(var i in o){
    if(typeof o[i] === 'object'){  //要考虑深复制问题了
      if(o[i].constructor === Array){
      //这是数组
        c[i] =[]
      }else{
      //这是对象
        c[i] = {}
      }
      deepCopy(o[i],c[i])
    }else{
      c[i] = o[i]
    }
  }
  return c
}
var result = {name:'result'}
result = deepCopy(china,result)
console.dir(result)
```

# 9. 数组去重
1. ES5
  - 方法一（计数排序的逻辑）：
    ```
    Array.prototype.distinct = function (){
     var arr = this,
      i,
      obj = {},
      result = [],
     for(i = 0; i< arr.length; i++){
      if(!obj[arr[i]]){ //如果能查找到，证明数组元素重复了
       obj[arr[i]] = 1;
       result.push(arr[i]);
      }
     }
     return result;
    };
    var a = [1,2,3,4,5,6,5,3,2,4,56,4,1,2,1,1,1,1,1,1,];
    var b = a.distinct();
    console.log(b.toString());     //1,2,3,4,5,6,56
    ```
  - 方法二：（递归）
    ```
    Array.prototype.distinct = function (){
     var arr = this,
     len = arr.length;
     arr.sort(function(a,b){  //对数组进行排序才能方便比较
       return a - b;
     })
     function loop(index){
       if(index >= 1){
         if(arr[index] === arr[index-1]){
         arr.splice(index,1);
       }
       loop(index - 1);  //递归
      }
     }
     loop(len-1);  //调用loop函数
     return arr;
    };
    var a = [1,2,3,4,5,6,5,3,2,4,56,4,1,2,1,1,1,1,1,1,56,45,56];
    var b = a.distinct();
    console.log(b.toString());  //1,2,3,4,5,6,45,56
    ```
方法一比较好
2. ES6
set数据结构
    ```
    function dedupe(array){
     return Array.from(new Set(array));
    }
    dedupe([1,1,2,3]) //[1,2,3]
    ```

# 10. 用正则实现string.trim()
```
function trim(string){
  return string.replace(/^\s+|\s+$/g,'') 
  //^\s+表示开头有一个或多个空格，|表示或，\s+$表示结尾
}
```

# 11. 什么是原型
举例：
```
//一个数组
let a = [1,2,3]
//a只有4个key:0,1,2,length
a.push(4)  //[1,2,3,4]
```
push方法哪来的？原型里的，数组是一个对象，每个对象都有一个隐藏的属性`__proto__`，而数组的隐藏属性指向数组的原型`Array.prototype`，push方法就存在这里面，可直接引用（还有pop,slice,splice）

# 12. class（类）
1. 类声明不会提升
2. 举例
```
class Rectangle {
    // constructor
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
    // Getter
    get area() {
        return this.calcArea()
    }
    // Method
    calcArea() {
        return this.height * this.width;
    }
}
const square = new Rectangle(10, 10);

console.log(square.area);
// 100
```
3. extends（继承）
```
class Animal { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}

var d = new Dog('Mitzie');
d.speak();  // 'Mitzie barks.'
```
# 13. JS如何实现继承
1. extends
见上面的extends
2. 原型链
```
function Animal(){
  this.body = '肉体'  //自身属性
}
Animal.prototype.move = function(){}  

function Human(name){
  Animal.apply(this,arguments)  //继承Animal的自身属性
  this.name = name
}

//下面这三句继承Animal的原型属性
let f = function(){}
f.prototype = Animal.prototype
Human.prototype = new f()

Human.prototype.useTools = function(){}  
//Human自己的原型属性
```
