---
title: HTTP面试
date: 2018-05-05 21:51:45
tags:
---
# 1. HTTP状态码
1开头的
>用于指定客户端应响应的某些动作

200 通常的成功 OK

204 成功处理请求，但不会刷新页面
> 表示服务器接收到的请求已经处理完毕，但浏览器页面不会刷新

301 永久重定向 Moved Permanently
> 请求的网页已永久移动到新位置，浏览器会转到另一个网址，永久性重定向与临时重定向不同的是，浏览器有可能会缓存，记住结果

302 Found
> HTTP/1.0就有的，临时性重定向，POST方法的重定向在未询问用户的情况下就会变成GET

303 和 307
> 这两个是HTTP/1.1新加的，都是临时重定向，303和302一样，POST重定向为GET。
307不同的是，把POST转为GET的。

304 Not Modified
> 表示资源未被修改过，还是返回和上次一样的东西

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

# 2. HTTP缓存（Cache-Control）
在服务器里设置
```
response.setHeader('Cache-Control', 'max-age=30')
```
每次浏览器请求完这个url后的30s内，都不会再请求这个文件。
但只要改变url，文件就会被再请求一次
所以css、js文件更新了，可以通过改变url来更新，例如
```
<script src="main.js"></script>  //第一个版本

<script src="main.js?v=2"></script>//第二个版本

<script src="main.js?随机数"></script>//以后的版本
```

# 3. Cache-Control和Etag的区别
1. ETag
设置响应头Etag
```
let string = fs.readFileSync('./main.js', 'utf8')
let fileMd5 = md5(string);
response.setHeader('ETag', fileMd5)
```
这样响应头的ETag中就会有该文件的md5值，浏览器会在请求头里设置if-None-Match，并附上这个md5值。
于是在请求的时候，如果这个md5值和你文件的md5值一样，说明文件没有更新，不需要下载
```
if(request.header['if-None-Match'] === fileMd5){
  response.statusCode = 304;
}
```

2. 和缓存的区别
缓存根本就不会发请求，而ETag会发请求，所以缓存更快

# 4. Cookie和Session
[cookie](https://www.jianshu.com/p/6bd8899154fc)   [seesion](https://www.jianshu.com/p/129a461c0779)
- Cookie
  1. HTTP响应通过Set-Cookie设置Cookie
  2. 浏览器访问指定域名必须带上Cookie作为Request Header
   3. Cookie一般用来记录用户信息
- Session
  1. session是服务器端的数据
  2. session一般通过在cookie里记录sessionID实现
  3. sessionID一般是随机数

# 5. LocalStorage和Cookie区别
[LocalStorage](https://www.jianshu.com/p/129a461c0779)
1. cookie会随请求被发送到服务器上，而localStorage不会
2. cookie大小一般在4k以下，localStorage在5Mb左右
3. localStorage一般被用来记录有没有提示过用户等信息，不能用来记录密码之类的

# 6. GET和POST的区别
1. 参数，GET的参数放在url的查询参数里，POST的参数（数据）放在请求消息体里
2. 安全，http协议下，POST比GET更安全
3. GET的参数有长度限制，一般是1024个字符，POST的参数一般没有长度限制(4-10Mb)
4. 包，GET请求只需要发一个包，POST要发两个以上包（因为有消息体）
5. GET用来读取数据，POST用来写数据，POST不幂等（幂等就是不管发多少请求，结果都一样，不幂等就是发一个请求，就多一条信息，数据库会越来越大）

# 7. 跨域
1. [JSONP](https://www.jianshu.com/p/dc7f20d5c2ab)
2. [CORS](https://www.jianshu.com/p/912600eba754)
3. postMessage
