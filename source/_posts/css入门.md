---
title: css入门
date: 2018-03-09 22:22:28
tags:
---
## 1. CSS简介
css2.1是目前世界上应用最广泛的版本，2011年开始css被分为多个模块单独升级，统称为CSS3，现在已经有很多模块升级到了CSS4。[css文档](https://www.w3.org/Style/CSS/specs.en.html)

## 2. 编写CSS的第一步
给你要写的css标签加上border
`border:1px solid red;`
让你知道它在哪、它的大小、形状

## 3. 使导航栏在同一行
当你想要一个列表排在同一行时，给所有li加上css`float:left;`，然后必须要给ul加上class:`clearfix`,下面是clearfix的css
```
.clearfix::after{
  content: "";
  display: block;
  clear: both;
}
```
但若ul是`display:fiex`，则要把clearfix去掉，因为clearfix的::after会占用一行里最后一小块空间
## 4. 高度
div（块级元素）：高度是由内部文档流元素高度的总和决定的。文档流：文档内元素的流动方向，内联元素是从左往右，块级元素是从上往下
 span（内联元素）：高度是由其中文字高度决定的，内联元素设置width和height是无效的，上下的margin和padding也无效，要将它们设为display:inline-block才有效。
## 5. 小提醒
尽量不写height和width，这两个属性会引出很多bug，要宽高的时候可以用padding，但img最好先写width，因为可以先占位，因为引用图片时浏览器不知道图片大小，所有等图片下载完成，它后面的元素又要重新排位置，若先写好width，则不用重排，知道height也可以先写好height。
另外span元素设置padding的时候要将它设为display:inline-block，因为内联元素不能设置宽高，inline-block具有inline的同行特性，也具有block的高度特性。
对于display:inline(内联元素)的元素，设置width/height/上下margin和padding都是无效的
## 6. 居中
1. 让一个背景图居中，并且让它自适应屏幕
```
background: url("wallhaven-w-min.jpg") no-repeat center center ;
background-size: cover;
```
2. 让一个div水平居中
```
margin-left:auto;
margin-right:auto;
```
3. 让一个div在父级元素中**绝对居中**（上下左右）
方法一：
给父级元素加:
   ```
   position:relative;   //若父级元素是body可以不用
   加
   ```
   再给div加：
   ```
   div{
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    margin: auto;
   }
   ```
   方法二：
给它的父元素加：
   ```
   display: flex;               //让它变成一个弹性盒
   justify-content: center;     //水平居中
   align-items: center;         //垂直居中
   ```
4. 让内联元素居中，给它们的父元素加上
    ```
    text-align:center;
    ```
    若不是内联元素想让它居中，则加display:inline-block，加了之后一般还要加下面这句，不然可能会有bug（下面可能会空出一行）
    ```
    vertical-align: top;
    ```
5. 让导航栏在同一行里均匀分布
给ul加css
```
ul{
  display:flex;  
  justyfy-content:space-between;
}
```
不用给li加`float:left`
也不用给ul加`clearfix`
## 7. 用css做三角形
1. 等腰三角形：
```
div{
  border:50px solid transparent;
  width:0;
  height:0;
  border-bottom-color:red;
}
```
2. 直角三角形：
```
div{
  border:50px solid transparent;
  width:0;
  height:0;
  border-top-width:0;
  border-left-color:red;
}
```

## 8. 怎样脱离文档流
1. 相对于窗口定位：
`position:fixed`
2. 相对于父级元素定位：
在父级元素加上：`position:relative`
给自己加上：`position:absolute  `（绝对定位后元素会变成display:block）

## 9. 使用::before和::after时
要加上这两行的代码，才会显示内容
```
content: "";
display:block;    //如果是绝对定位就不用加，因为绝对定位后元素会变成display:block;
```

## 10. 图片的轮播
\<html\>
```
<div class="window">
    <div class="images" id=images>
        <img1>
        <img2>
        <img3>
    </div>
</div>
```
\<css\>
**要给window的div和每个img都定好宽高！并给window加上overflow:hidden**
```
.images{
    display: flex;    //给image的div加上这个图片才能横这放！
}
.images > img{
    width: 100%;
}
```

