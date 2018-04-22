---
title: Cookie入门
date: 2018-04-22 00:01:54
tags:
---
# 1. 看一遍注册登陆的代码
- [github](https://github.com/Pengyize/homework/tree/master/sign-up)
- Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 Cookie 的过期时间
- 大小大概在 4kb 以内

# 2. 以注册登陆为例
1. 你注册账号时，浏览器发送post请求将你的用户名、密码发送给服务器，服务器会把你的用户名、密码存入数据库，即注册成功。
2. 在你登陆的时候，浏览器同样发送post请求，服务器会把你的账号密码和数据库里的匹配，若匹配成功，服务器会发送一个响应头给浏览器，例如：
`Set-Cookie: sign_in_email=xxx@xxx.com`
这里面记录着你的登陆信息，浏览器会把这个cookie保存下来
3. 当你在一定时间内访问这个域名时，浏览器会带着这个cookie发送GET请求，服务器接收到请求后发现cookie里的信息和数据库里可以匹配上，于是服务器会直接发送给你已经登陆的网页
4. 浏览器在一段时间后会自动删除cookie，若发送请求时没有cookie，或cookie里的信息和服务器的数据库不匹配，则不会登陆

# 3. 用户可以随意更改cookie
所以cookie不安全，但session可以解决这个问题