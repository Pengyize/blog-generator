---
title: 配置HEXO博客-linux
date: 2018-02-28 10:02:26
tags:
---
###### 1. 第一次创建博客
a. 终端进入Desktop目录
b. github上新建一个空的repo，名字是[你的用户名.github.io]
c. 运行`npm install -g hexo-cli`安装 Hexo 
d. `hexo init myBlog`
e. `cd myBlog`
f. `npm i`
g. `hexo new 开博大吉`，创建了一篇博客
h. 复制这篇博客的路径，`vi 路径`进行编辑
i. `vi _config.yml`，把 title 改成想要的名字，把author 改成你的名字，把最后一行 type 改成 type: git（git前有空格），在最后一行后新增一行，左边与 type 平齐，加上 repo: 仓库SSH地址（地址前有空格）
j.`npm install hexo-deployer-git --save`
k. `hexo deploy`
l. 若出现Error
`Permission denied (publickey).`
`fatal: 无法读取远程仓库。`，则按[这里](https://stackoverflow.com/questions/19660744/git-push-permission-denied-public-key)的方法解决
m. 进入对应的 repo，点setting，将GitHub Pages 功能中的source改成master branch，点save，点击预览链接
n. `hexo new 名字`建立第二篇博客 
o. `vi 路径`进行编辑
p. `hexo g`
q. `hexo d` 完成第二篇上传～
###### 2. 删除文章
先在本地删除，然后进入博客目录依次
a. `hexo g`
b. `hexo d`
###### 3. 下载已有的博客
a. 终端进入Desktop
b. 复制源代码仓库的SSH地址，`git clone 源代码地址`
c. 进入下载的目录 `npm install hexo --save`
d. 就可以按照上面1.m的方法创建新博客了

###### 4.第一次建立博客后创建源代码仓库
1.创建名叫 blog-generator 的空仓库
2.按图中在终端进入你的博客目录中执行！用SSH地址！ [图片上传失败...(image-5d7caf-1519746300959)]
3.以后每次 hexo deploy 完之后，博客就会更新；然后你还要要 add / commit /push 一下，以防万一。
