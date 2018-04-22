---
title: 实现AJAX
date: 2018-04-13 17:58:04
tags:
---
# 1. 原生JS实现AJAX
第一步：`let request = new XMLHttpRequest();`
### 1. 设置请求
用AJAX设置请求的第一部分：
```
request.open('get','/xxx')  //设置get的请求方式，再设置路径为/xxx
```
设置第二部分：
```
request.setRequestHeader('Accept','text/html')
```  
设置第四部分：
```
request.send('请求体')  //请求一般没有第四部分，可以直接send空字符串
```

### 2. 获取响应
获取HTTP状态码
```
request.status  //200
request.statusText  //OK
```
获取响应第二部分
```
request.getAllResponseHeaders()  //获取第二部分所有
request.getResponseHeader('Content-Type')  //获取Content-Type
```
获取第四部分
```
requeset.responseText
```

# 2. jQuery实现AJAX
1. 封装ajax
```
jQuery.ajax=function({url,method,body,headers}){
  return new Promise(function(resolve,reject){
    let request = new XMLHttpRequest()
    request.open(method,url)  //配置request
    for(let key in headers){
      let value = headers[key];
      request.setRequestHeader(key,value);
    }
    request.onreadystatechange = ()=>{
      if(request.state === 4){
        if(request.status >= 200 && request.status < 300){
          resolve.call(undefined,request.responseText)
        }else if{request.status >= 400}{
          reject.call(undefined,request)
        }
      }
    }
    request.send(body);  //body是第四部分
  })
}
```
返回一个promise对象，传入的两个参数resolve、reject，分别代表成功时执行的内容和失败时执行的内容，下面的then就是使用promise。

2. 使用ajax
```
$.ajax({
  url: '/xxx',
  method: 'get',
  headers:{
    'content-type':'application/x-www-form-urlencoded',
    'pyz':21
  }
}).then(
  (responseText) =>{
    console.log(responseText);  
    return responseText;  //上面的返回的是成功就执行这个，失败就执行下面那个
  },
  (request)=>{
    console.log('error'); return 'error'  //失败就执行这个
  }
)
```