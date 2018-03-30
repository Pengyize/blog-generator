---
title: JavaScript Dom入门
date: 2018-03-25 23:32:07
tags:
---
# 1. JS初级主要就两个作用：
>1.找元素
2.给元素增加/删除class

# 2.
```
Node.ELEMENT_NODE === 1  //true，元素节点
Node.TEXT_NODE === 3     //true，元素中的文本

xxx.nodeType === 3       //可用来检验xxx是一个元素节点还是元素中的文本
```

# 3. 
ul的tagName为'UL'（大写！）

`let brother = li.getElementsByTagName('UL')[0];`
getElementsByTagName这个API搜索的是li元素的后代，并按顺序返回所有的ul，返回的是一个数组，要写上[0]

# 4. 
```
a.href     //这样获取href，浏览器会给href加上http协议
a.getAttribute('href')  //这样获取的才是href本身

```

# 5.
```
liTags[i].onmouseenter = function (x) {
      console.log(x.target);       //x.target是我们操作的那个元素，若a里包含了个span，那操作的就是span
      console.log(x.currentTarget) //x.currentTarget是我们监听的元素，就是liTags[i]这个元素
}
```

# 6.
用JS完成页面内的跳转
```
let aTags = document.querySelectorAll('nav.menu > ul > li > a');   //获取所有a标签，返回的是一个数组
for(let i=0;i<aTags.length;i++) {     //因为aTags是数组，所以要用for循环，同时监听到数组里的所有元素
    aTags[i].onclick = function (x) { //监听a标签被鼠标点击的动作
        x.preventDefault();           //防止默认动作（跳转）
        let a = x.currentTarget;      //当前监听的元素a
        let href = a.getAttribute('href');  //获取a的href值
        let element = document.querySelector(href);  //获取带有这个href值的标签 例：'#siteAbout'
        let top = element.offsetTop; //获取这个标签的底端到整个页面顶端的距离（固定值）
        window.scrollTo(0,top);  //跳转window.scrollTo(x,y);
    }
}
```

# 7. console.log调试大法
出问题了就在每一步console.log，能解决很多问题

# 8. setInterval()
```
let i=0;
let say = setInterval(() => {
            if(i === 25){
                window.clearInterval(say);      //调用setInterval的名字来停止它
                return;
            }
            i++;
           console.log(i);    //从1报数到25，一秒一次，到25就停
        },1000);
```

# 9. Tween.js
[缓动动画速查表](http://easings.net/zh-cn)
1. 在[cdn](cdnjs.com)里搜tween，并在html中引用
2. 在[github-tween](https://github.com/tweenjs/tween.js/)中查看使用教程
 
# 10. 选择器
```
let a = document.querySelector('a[href="' + id + '"]')
//href外要包一个中括号，地址外要包一个双引号！并且变量id要和其他的用加号隔开
```

# 11. 儿子选择器
 ```
var c = div.children;    //会获得div下的所有子标签
var c = div.childNodes;  //会获得div下的所有子标签加文本标签
```

# 12. 获得所有兄弟姐妹
方法一：
```
var getSiblings = function (elem) {
	var siblings = [];
	var sibling = elem.parentNode.firstChild;
	for (; sibling; sibling = sibling.nextSibling) {
		if (sibling.nodeType !== 1 || sibling === elem) continue;
		siblings.push(sibling);
	}
	return siblings;
};
```
方法二 用getSiblings()：
```
var elem = document.querySelector('#some-element');
var siblings = getSiblings(elem);
```
