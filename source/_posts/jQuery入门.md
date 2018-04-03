---
title: jQuery入门
date: 2018-04-03 23:57:23
tags:
---
# 1. 引用
[jquery下载页面](https://jquery.com/download/)，下载为js文件，在html中引用即可

# 2. 基础
jQuery的原型为jQuery.prototype
```
var div = document.getElementById('x')  //dom对象
var $div = $('#x')  //jquery对象
```
div和$div的联系：`$div[0] === div`
`$div === $(div)`
区别：div是id为x的元素
&div是对象
# 3. API
```
$nodes.addClass('red');
$nodes.addClass(function(index,currentClass){
      return 'sd-'+index;    //这样nodes里每一项会依次添加sd-0 sd-1 sd-2 sd-3 ......的class
    });  
var classes = ['red','blue','black'];
$nodes.addClass(function(index,currentClass){
      return classes[index];    //前三项就会添加red、blue、black的class
    });  

$nodes.removeClass('red');

$(x).on('click', function(){    //建一个button并给它id为x
    $nodes.toggleClass('red');  //每点一次button，nodes就增加或删除'red'class
})
```
# 4. jQuery对象和DOM对象的转换
jquery转dom
```
var div = $div[0]  //这样jquery就转换成了DOM对象，或div = $div.get(0)
```
dom转jquery
```
var $div = &(div);  //这样dom对象div，就转换成了jquery对象
```
