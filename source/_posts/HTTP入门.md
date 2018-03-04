---
title: HTTP入门
date: 2018-03-02 16:47:09
tags:
---
### 1. HTTP(HyperText Transfer Protocol)
是一种协议，它教客户端如何请求、服务器如何响应。

### 2. 状态码
是服务器对浏览器说的话：
200，通常的成功（GET）
204，创建成功（POST）
301，网站永久的搬走了
302，网站暂时不能访问（备案、被查）
304，滚吧，返回和上次一样的话
404，你（访问者）错了
5xx，服务器错了

### 3. 请求的格式
1 GET或POST   路径(/)   协议(HTTP)/版本号
2 Host: www.baidu.com
2 key: value
2 ....: ....
....
3（断行）
4  要上传的数据

### 4.响应的格式
1 协议(HTTP)/版本号  状态码  状态解释
2 key: value
2 Content-Length: ...
2 Content-Type: text/html或application/x-JavaScript
3 （断行）
4 下载的内容

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