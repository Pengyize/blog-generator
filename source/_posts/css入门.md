---
title: css入门
date: 2018-03-09 22:22:28
tags:
---
## 1. CSS简介
css2.1是目前世界上应用最广泛的版本，2001年开始css被分为多个模块单独升级，统称为CSS3，现在已经有很多模块升级到了CSS4。[css文档](https://www.w3.org/Style/CSS/specs.en.html)

## 2. 使几个元素在同一排
当你想要一个列表排在同一排时，给那几个元素全加上style=float:left/right，然后给他们的父元素加上class:clearfix。
```
.clearfix::after{
  content: "";
  display: block;
  clear: both;
}
```
## 3. 高度
div（块级元素）：高度是由内部文档流元素高度的总和决定的。文档流：文档内元素的流动方向，内联元素是从左往右，块级元素是从上往下
 span（内联元素）：高度是由其中文字高度决定的
## 4. 小提醒
尽量不写height和width，会引出很多问题，要宽高的时候用padding，另外span元素设置宽高的时候要将它设为display:inline-block，因为内联元素是不能设置宽高的，inline-block具有inline的同行特性，也具有block的高度特性。
对于display:inline(内联元素)的元素，设置width/height/上下margin和padding都是无效的

## 5. 居中
1. 若想让一个背景图居中，并且让它自适应屏幕
```
background: url("wallhaven-w-min.jpg") no-repeat center center ;
background-size: cover;
```
2. 若想让一个div水平居中，则加
```
margin-left:auto;
margin-right:auto;
```
3. 若想让内联元素居中，给它们的父元素加上
```
text-align:center;
```
若不是内联元素想让它居中，则加display:inline-block，加了之后一般还要加下面这句，不然可能会有bug（下面空出一行）
```
vertical-align: top;
```
4. 若想让一个东西在它的父元素中绝对居中（上下左右）则给它的父元素加：
```
display: flex;               //让它变成一个弹性盒
justify-content: center;     //水平居中
align-items: center;         //垂直居中
```

## 6. 用css做三角形
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

## 7. 怎样脱离文档流
1. 相对于窗口定位：
`position:fixed`
2. 相对于父级元素定位：
在父级元素加上：`position:relative`
给自己加上：`position:absolute  `（绝对定位之后就会变成display:block）

## 8. 用::before和::after时
加上
```
content: "";
display:block;
```
这样才会显示内容
