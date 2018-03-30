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
> GET：请求的对应资源会作为响应返回。响应将包含描述或操作的结果。
POST：返回处理对应请求的结果。

204 成功处理请求，没有返回任何内容 No Content
> 表示服务器接收到的请求已经处理完毕，但是服务器不需要返回响应。比如，客户端是浏览器的话，那么浏览器显示的页面不会发生更新。

206 Partial Content
> 成功处理了部分GET请求


301 Moved Permanently
> 请求的网页已永久移动到新位置，永久性重定向


302 Found
> 网站临时性重定向，暂时不能访问（备案、被查）

303 See Other
> 该状态码表示由于请求对应的资源存在另一个URI，并指定必须使用GET方法定向获取请求的资源。和302不同的是，302是不会改变上次的请求方法

304 Not Modified
> 访问不了，并返回和上次一样的话,表示资源未被修改过，还是和上次访问时一样。

307 Temporary Redirect
> 临时重定向，和302、303类似，不同的是，不会指定客户端要用什么样的方法请求，

400 Bad Request
> 表示客户端中存在语法错误，导致服务器无法理解该请求。客户端需要修改请求的内容后再次发送请求。

401 Unauthorized
> 即用户没有必要的凭据。该状态码表示当前请求需要用户验证。

403 Forbidden
> 服务器已经理解请求，但是拒绝执行它。

404 Not Found
> 服务器找不到请求的网页。


500 Internal Server Error
> 服务器遇到错误，无法完成请求。

503 Service Unavailable
> 由于临时的服务器维护或者过载，服务器当前无法处理请求。这个状况是暂时的.


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

   username=pyz&password=123

**请求里的路径只是路径而已，跟文件没有关系，文件格式只和Accept里写的有关系！！**
### 4.响应的格式
1. GET的响应
HTTP/1.1 200 OK
Content-Length: ...
Content-Type: text/html或application/x-JavaScript; charset=utf-8
（断行）
<!DOCTYPE html>
<html>...</html>

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