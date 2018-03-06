---
title: HTML元素
date: 2018-03-06 08:36:58
tags:
---
## 1. iframe 和 a 的target
iframe标签支持相对路径

`<iframe name="xxx" src="" frameborder="0"></iframe>  `
`<a href="" target="xxx"></a>`点击a
则会在iframe里弹出
index里写:
`<iframe src="./index2" frameborder="0"></iframe>  `则会在左上角出现一个小的嵌套页面显示index2里嵌套的index3里的四个QQ链接
index2里写:
`<iframe src="./index3" frameborder="0"></iframe>`
index3里写:
`<a href="http://qq.com" target=_blank>QQ</a>`点击会在一个新的标签页面里打开
`<a href="http://qq.com" target=_self>QQ</a>`点击会在index3的嵌套页面打开
`<a href="http://qq.com" target=_parent>QQ</a>`点击会在index2的嵌套页面打开
`<a href="http://qq.com" target=_top>QQ</a>`点击会在index1里打开

## 2. a 的href
1. `<a href="//qq.com">QQ</a>`href里写的是无协议地址，意思是当前用的是http协议就自动继承http协议，用的是file就会用file协议。
我们在终端运行`sudo npm i -g http-server`即可安装一个服务器，进入你写index.html的文件夹里运行`http-server`即可开启服务器，然后在浏览器浏览终端返回的地址即可用http协议来访问你写的文件

2. `<a href="?name=pyz">qq</a>`点击之后会在当前页面发起?name=pyz的请求
`<a href="#sss">qq</a>`点击之后不会发起请求，因为锚点仅仅是在当前页面内的跳转
**`<a href="/..">link</a> 标签被点击后会浏览器会发起GET / HTTP/1.1的请求，因为/是根，无法再..**
3. 伪协议
 `<a href="javascript:;">qq</a>`点击之后a不会做任何事情
`<a href="javascript:alert(1)";>qq</a>`点击之后会弹出1

## 3. form input
**1. form 和 a 的区别：**
a提交时是GET请求
form可以发送POST请求
form里必须要有一个submit才能被提交
```
<form action="users" method="post">
    <input type="text"value="username">
    <input type="password"value="password">
    <input type="submit" value="提交">
</form>
```
即form是注册时用的，你提交的账号密码会出现在第四部分里，但GET请求是不会有第四部分的，POST若想有查询参数，可以直接写在action里，如；
```
<form action="users?name=pyz" method="post">
    <label>用户名<input type="text" name="username"></label>
    <label>密码<input type="password" name="password"></label>
    <input type="submit" value="提交">
</form>
```
**input要提交的话一定要有name值！**
label可以直接包在input外面
form里的target和a是一模一样的。
form里如果没有`<input type="submit">`而有<button>，则button会默认为submit，若写成这样`<button type="button">button</button>`则不会成为submit，一个form里必须要有一个submit才能提交

** 2. input的checkbox属性**
 
```
<label><input type="checkbox" name="apple" value="yes">苹果</label>
<label><input type="checkbox" name="banana" value="yes">香蕉</label>
```
![<checkbox>](/images/checkbox.png)

一定要有name才能被提交上去

![提交之后](/images/提交之后.png)

** 3. input radio**
```
<label><input type="radio" name="sexual">男</label>
<label><input type="radio" name="sexual">女</label>
```
和checkbox不同的是，两个name一样的radio只能选中一个

![<radio>](/images/radio.png)

## 4. select
```
<select name="group" multiple>
    <option value="">-</option>
    <option value="1">第一组</option>
    <option value="2">第二组</option>
    <option value="3" disabled>第三组</option>
    <option value="4" selected>第四组</option>
</select>
```
![<select>](/images/select.png)disabled属性意味着不能被选中，selected意思是默认选中的，multiple意思是可以同时选中几项

## 5. textarea
若想让用户输入一大段文字则用这个元素
```
<textarea style="resize: none; width: 200px; height: 100px;"  name="hobbies"></textarea>
```
![<textarea>](/images/textarea.png)
resize若不设置为none，则用户可以随意更改输入框的大小

## 6. table
```
<table border="1">
    <colgroup>
        <col width="100">
        <col bgcolor="red" width="200">
        <col width="100">
        <col width="100">
    </colgroup>
    <thead>
        <tr>
            <th>项目</th><th>姓名</th><th>班级</th><th>成绩</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th></th><td>可爱多</td><td>1</td><td>22</td>
        </tr>
        <tr>
            <th></th><td>金钟国</td><td>2</td><td>12</td>
        </tr>
        <tr>
            <th>平均分</th><td></td><td></td><td>17</td>
        </tr>
    </tbody>
    <tfoot>
    <tr>
        <th>总分</th><td></td><td></td><td>34</td>
    </tr>
    </tfoot>
</table>
```
![<table>](/images/table.png)
thead  tbody tfoot不写浏览器也不会报错，而会自动全部加入到tbody里