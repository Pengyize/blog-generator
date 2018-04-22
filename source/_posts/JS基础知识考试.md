---
title: JS基础知识考试
date: 2018-04-18 09:32:07
tags:
---
# 1. 关于new
```
function fn(){
    console.log(this)
}
new fn()  //会执行fn
```
答：this就是fn，它有`__proto__`属性，`__proto__`指向这个fn的原型
fn的原型里有两个属性`{contructor: fn()}`和`__proto__`(指向Object.prototype)

# 2. MVC
1. MVC是Model View Controller
View：是这个js模块对应在html中的部分，就是展示给用户看的那一部分

    Model：可以从服务器获得数据，把数据传给Controller。还要将Controller监听到的用户提交的数据上传到服务器。

    Controller：调用model的数据，用来更新view。还要监听用户在view上的操作，获取用户提交的数据，传给model。

2. 代码
```
window.Model = function(options){
    let resourceName = options.resourceName;
    return {
        init : function(){},
        fetch: function(){},
        save: function(){}
    }
}

window.View = function(selector){
    return document.querySelector(selector);
}

window.Controller = function(options){
    let init = options.init;

    let object = {
        view: null,
        model: null,
        init: function(view,model){
            this.view = view;
            this.model = model;
            this.model.init();
            init.call(this.view);
            this.bindEvents.call(this)
        }
    };
    for(let key in options){
        if(key !== 'init'){
            object[key] = options[key]
        }
    }
    return object;
}
```
# 3. 用函数模拟一个类
```
function Animal(species) {
    this.species = species; //自有属性
}
    
Animal.prototype = {
    constructor: Animal,
    walk : function () {},  //走路的代码
    run: function () {},    //跑步的代码
    eat: function () {},    //吃东西的代码
    sleep: function () {}   //睡觉的代码
};

let cat = new Animal('cat')
cat.specise === cat     //true
//并且cat对象的__proto__指向Animal.prototype，有里面的动作属性
```
# 4. promise
```
promiseTest = function (a,b){
    return new Promise(function(resolve,reject){
        if(a+b>5){
            resolve();  //若参数a+b大于五则执行resolve
        }else{
            reject();   //若参数a+b大小于等于五则执行resolve
        }
    })
}
```
使用：
```
promiseTest(4,6).then(
    () => {
        console.log('大于5');
    },
    () => {
        console.log('小于5')
    },
)   //'大于5'
```

# 5. JSON
[AJAX入门](https://www.jianshu.com/p/912600eba754)