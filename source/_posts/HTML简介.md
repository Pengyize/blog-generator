---
title: HTML简介
date: 2018-03-06 08:36:09
tags:
---
html没有块级元素和内联元素的区别，意思就是html只管内容，不管样式，所有样式都由css决定

### 1.W3C简介
万维网联盟（W3C）由[李爵士](https://zh.wikipedia.org/wiki/%E6%8F%90%E5%A7%86%C2%B7%E6%9F%8F%E5%85%A7%E8%8C%B2-%E6%9D%8E "蒂姆·伯纳斯-李")于1994年10月离开[欧洲核子研究中心](https://zh.wikipedia.org/wiki/%E6%AD%90%E6%B4%B2%E6%A0%B8%E5%AD%90%E7%A0%94%E7%A9%B6%E7%B5%84%E7%B9%94 "欧洲核子研究中心")（CERN）后成立，该组织通过W3C制定的新标准来促进业界成员间的兼容性和协议。联盟试图让所有的供应商实施一套由联盟选择的核心原则和组件。

### 2.MDN简介
**MDN Web Docs**（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多[Mozilla基金会](https://zh.wikipedia.org/wiki/Mozilla%E5%9F%BA%E9%87%91%E6%9C%83 "Mozilla基金会")产品和网络技术开发文档的免费网站。
MDN网站上有目前较全的前端基础教学，如HTML、CSS、JS等
[HTML元素表](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)

### 3.空标签
空标签就是不用加闭标签的标签，也可以叫闭元素。如：
*   [`<area>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/area "HTML <area> 元素 在图片上定义一个热点区域")
*   [`<base>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/base "HTML <base> 元素 指定用于一个文档中包含的所有相对URL的基本URL。一份中只能有一个<base>元素。")
*   [`<br>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/br "HTML 元素 换行 <br> 在文本中产生一个换行（回车键）。这对于写诗或写一个地址来说显得很有用。它可以将行明显地分开。")
*   [`<col>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/col "HTML <col> 元素 定义表格中的列，并用于定义所有公共单元格上的公共语义。它通常位于<colgroup>元素内。")
*   [`<colgroup>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/colgroup "HTML 中的 表格列组（Column Group <colgroup>） 标签用来定义表中的一组列表。") when the [span](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/colgroup#attr-span) is present
*   [`<command>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/command "command元素用来表示一个用户可以调用的命令.")
*   [`<embed>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/embed "HTML <embed> 元素 用于表示一个外部应用或交互式内容的集合点，换句话说，就是一个插件。")
*   [`<hr>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/hr "HTML <hr> 元素表示段落级元素之间的主题转换（例如，一个故事中的场景的改变，或一个章节的主题的改变）。在HTML的早期版本中，它是一个水平线。现在它仍能在可视化浏览器中表现为水平线，但目前被定义为语义上的，而不是表现层面上。")
*   [`<img>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img "HTML Image 元素（ <img> ）代表文档中的一个图像。")
*   [`<input>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input "HTML <input> 元素用于为基于Web的表单创建交互式控件，以便接受来自用户的数据。")
*   [`<keygen>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/keygen "HTML <keygen> 元素是为了方便生成密钥材料和提交作为 HTML form 的一部分的公钥.这种机制被用于设计基于 Web 的证书管理系统。按照预想，<keygen> 元素将用于 HTML 表单与其他的所需信息一起构造一个证书请求，该处理的结果将是一个带有签名的证书。")
*   [`<link>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link "HTML 中<link>元素指定了外部资源与当前文档的关系. 这个元素的使用方法包括为导航定义关系框架.这个元素经常用来链接css文件。")
*   [`<meta>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta "HTML <meta> 元素表示那些不能由其它HTML元相关元素 (<base>, <link>, <script>, <style> 或 <title>) 之一表示的任何元数据信息.")
*   [`<param>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/param "HTML <param> 元素(或 HTML Parameter 元素) 定义了 <object>的参数")
*   [`<source>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/source "The HTML <source> element specifies multiple media resources for either the <picture>, the <audio> or the <video> element. It is an empty element. It is commonly used to serve the same media content in multiple formats supported by different browsers.")
*   [`<track>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/track "HTML <track> 元素 被当作媒体元素—<audio> 和 <video>的子元素来使用。它允许指定计时字幕（或者基于事件的数据），例如自动处理字幕。")
*   [`<wbr>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/wbr "HTML <wbr> 元素  — 一个文本中的位置，其中浏览器可以选择来换行，虽然它的换行规则可能不会在这里换行。")

### 4.可替换标签
宽高由自己决定的元素，如：
`<img>`
`<video>`
`<input>`