---
title: HTTP入门
date: 2018-03-02 16:47:09
tags:
---
### 1. HTTP(HyperText Transfer Protocol)
http是超文本传输协议，它教客户端如何请求、服务器如何响应。

### 2. 状态码（背下来）
是服务器对浏览器说的话：

200 通常的成功 OK

204 成功处理请求，但不会刷新页面
> 表示服务器接收到的请求已经处理完毕，但浏览器页面不会刷新

301 永久重定向 Moved Permanently
> 请求的网页已永久移动到新位置，永久性重定向


302 Found
> HTTP/1.0就有的，临时性重定向，POST方法的重定向在未询问用户的情况下就会变成GET

303 和 307
> 这两个是HTTP/1.1新加的，都是临时重定向，303和302一样，POST重定向为GET。
307不同的是，把POST转为GET的。

304 Not Modified
> 表示自从上次请求后，网页未被修改过 

400 Bad Request
>客户端中存在语法错误。

401 Unauthorized
> 用户未授权，需要用户验证。

403 Forbidden
> 服务器已经理解请求，但拒绝执行

404 Not Found
> 服务器找不到请求的网页。


500 Internal Server Error
> 服务器遇到错误，无法完成请求。

503 Service Unavailable
> 由于临时的服务器维护或者过载，暂时无法处理请求


**背下来**


### 3. 请求的格式（背下来）
1. GET请求
GET / HTTP/1.1
Host: baidu.com
Accept: text/html
（断行）

2. POST请求
POST /login HTTP/1.1
Host: baidu.com
Accept: application/json
Content-Type: application/x-www-form-urlencoded
Content-Length: ...

   username=pyz&password=123（第四部分服务器返回的是字符串）

**请求里的路径只是路径而已，跟文件没有关系，文件格式只和Accept里写的有关系！！**
### 4.响应的格式
1. GET的响应
HTTP/1.1 200 OK
Content-Length: ...
Content-Type: text/html或application/x-JavaScript; charset=utf-8
（断行）      => 这是第三部分
<!DOCTYPE html>
<html>...</html>（第四部分服务器返回的是字符串）

2. POST
若密码错了
HTTP/1.1 401 Unauthorized（若成功了就是200 OK）
Content-Type: application/json
Content-Length: ...

   {''error"}


### 5. 如何查看响应和请求
1. 打开Network
2. 刷新网址
3. 选中第一个响应
4. 查看Headers里的Response Headers点view source可以看到响应的前两部分，Request Headers点view source可以看到请求
5. 查看Response你可以看到响应的第四部分

### 6. DNS(Domain Name System)
DNS即是通过域名找IP地址
有两个命令：
`nslookup www.baidu.com`
`ping www.baidu.com`
输入这两个命令都会返回baidu的IP地址![nslookup](/images/nslookup.png)Server你的路由，相当于路由问了电信公司，于是下面返回的就是baidu的IP地址（baidu有很多台服务器，会返回离你最近几台服务器的IP）。
可以通过修改你电脑上的hosts文件，绕过DNS，直接指定一个域名的IP（因为有时候电信会给你假IP）
修改hosts文件，mac终端：`vi ~/etc/hosts`
在里面添加一行
123.123.123 baidu.com
保存退出，再ping baidu.com，返回的就会是123.123.123了，这样就绕过了DNS