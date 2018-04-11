---
title: AJAX入门
date: 2018-04-11 21:41:44
tags:
---
# 1. 历史
### 1. 如何发请求
- form可以发送GET和POST请求，会刷新页面或新开页面
- a可以发送GET请求，会刷新页面或新开页面
- img可以发送GET请求，只能以图片形式展示
- link可以发送GET请求，只能以css或favicon形式展示
- script可以发送GET请求，只能以脚本形式运行
### 2. 进化
IE5在JS中引入ActiveX对象(API)，使JS可以直接发送请求，其他浏览器跟进，取名XMLHttpRequest，被纳入W3C规范。现在进化成AJAX

# 2. AJAX
Jesse James Garrett将这个技术取名为AJAX：异步的JavaScript和XML。
1. 使用XMLHttpRequest发请求
2. 服务器返回XML格式的**字符串**，只能返回字符串
3. JS解析XML，并更新局部页面

**API：**`readyState === 4    //表示整个请求过程已完毕`

# 3. 用的是JSON
### 1. JSON是抄袭了JavaScript的一门语言
**区别：**
1. JSON没有抄袭function和undefined
2. JSON的字符串首尾必须用双引号"pyz" 
3. JSON有6种数据类型
- null
- number
- string（必须用双引号）
- true
- false
- array（["a","b"]）
- object（{"name":"pyz"}）
4. JSON没有symbol，没有函数，没有undefined，也没有原型。
### 2. API
```
1. let request = new XMLHttpRequest();
2. request.open('GET','/xxx')  //初始化request
3. request.send()  //发送请求
4. request.onreadystatechange  //监听请求状态的变化
5. request.readyState === 4  //说明响应完成
6. request.status  //响应返回的HTTP状态码
7. var string = request.responseText  //响应的内容
1. var value = JSON.parse(request.responseText)  //把符合JSON语法的字符串转换成JS，解析响应返回的内容
2. value.node   //若value是对象，这就是对象里内容
3. value.node.name  //对象里的name的值
```

# 4. 同源策略
1. form、img、script等上面提到的请求方式，是可以对别的域名发送请求的。
但用AJAX不能对别的域名放送请求，只有协议、域名、端口号**一摸一样**才允许发送AJAX（多个www是不同的域名）
因为AJAX是可以获取响应内容的，如果没有同源策略的限制，别的网站可以通过AJAX获取另一个网站的所有信息。
2. AJAX可以通过**CORS**发送请求到别的网站
**跨域资源共享：Cross-Origin Resource Sharing**
在需要访问的服务器里添加一句
    ```
    response.setHeader('Access-Control-Allow-Origin', 'http://pyz.com:8888')
    ```
    `http://pyz.com:8888`是我的协议+域名+端口号，这样我就可以访问他的服务器了，即使我们域名不同
    ```
    response.setHeader('Access-Control-Allow-Origin', '*')  //这样这个服务器就可以接受所有网站的AJAX请求
    ```
# 5. 面试题
**请使用原生JS发送AJAX**
```
let request = new XMLHttpRequest();
request.open('GET','/xxx');
request.send();
request.onreadystatechange = ()=>{
  if(request.readyState === 4){
    if(request.status >= 200 && request.status < 300){
      var string = request.responseText;
      var value = JSON.parse(string);
    }
  }
}
```