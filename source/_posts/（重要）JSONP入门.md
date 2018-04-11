---
title: （重要）JSONP入门
date: 2018-04-10 16:14:42
tags:
---
# 1. 必考面试，什么是JSONP
请求方：frank.com的前端程序员（浏览器）
响应方：jack.com的后端程序员（服务器）
1. 请求方用JS创建一个script标签，它的src指向响应方，同时传查询参数(?callback=...)，如下
```
script.src = 'http://jack.com:8002/pay?callback=' + functionName;
```
并用`document.body.appendChild(script)`将它添加进页面中
2. 响应方通过查询参数callback构造
     ` functionName.call(undefined,'数据')`
    这样的响应
3. 浏览器接到响应就会执行 ` functionName.call(undefined,'数据')`
4. 那么请求方就知道了他想要的数据，'success' or 'fail'

以上就是JSONP

` functionName.call(undefined,'数据')`
'数据'叫做JSON，'数据'左边的叫JSON的左padding，右边的括号叫右padding，合起来叫JSONP

# 2. 必考面试题：JSONP为什么不支持POST请求
答：因为JSONP是通过动态创建script的方法进行的，而script只能发送get请求不能发送post请求。

# 3. jquery的写法
```
$.ajax({
        url:"http://jack.com:8002/pay",
        dataType: "jsonp",
        success:function (response) {
            if(response === 'success'){
                amount.innerText = amount.innerText-1;
            }
        }
    })

```