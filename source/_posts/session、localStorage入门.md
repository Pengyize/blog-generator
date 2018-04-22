---
title: session、localStorage入门
date: 2018-04-23 00:37:08
tags:
---
# 1. 由于用户可以随意更改cookie
因为登陆信息暴露给了用户，所以cookie不安全，用session解决这个问题。
session是依赖于cookie的，服务器将发给浏览器的响应头`Set-Cookie`里的信息替换为一个随机数sessionID，并把cookie里的信息存在服务器内存的session表里。
浏览器访问服务器时，服务器通过sessionID来查找cookie对应的信息，而暴露给用户的只有一个sessionID，很安全。

# 2. localStorage
1. - 与cookie不同，请求的时候浏览器不会带上localStorage
    - 而且每个域名localStorage最大存储量5Mb左右，cookie只有4k左右
    - 而且localStorage理论上不会过期，除非清理缓存
    - 所以持续化存东西的时候用localStorage
2. session是服务器上的hash，localStorage是浏览器上的hash，localStorage里存的东西保存在本地。
3. 只有相同域名的网页才能互相读取localStorage。
4. **API:**
```
localStorage.setItem('a',1);
localStorage.getItem('a');    //1
```
5. 用来记录有没有提示过用户等信息，不能用来记录密码之类的

# 3.  sessionStorage
sessionStorage和session没有关系，sessionStorage和localStorage的1、2、3是一样的，区别是关掉浏览器后就会被清除