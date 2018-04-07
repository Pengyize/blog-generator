---
title: SASS入门
date: 2018-04-06 16:06:56
tags:
---
# 1. 安装（mac）
我安装的是node-sass
在命令行里进入~目录，输入：
- `npm config set registry https://registry.npm.taobao.org/`
- `echo 'export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass"'>> ~/.bashrc`(若是用的zshrc则改为~/.zshrc)
- `source ~/.bashrc`(同上)
- `sudo cnpm i -g node-sass`（需要先安装cnpm）
- `mkdir ~/Desktop/scss-demo`
- `cd ~/Desktop/scss-demo`
- `mkdir scss css`
- `touch scss/style.scss`
- `node-sass -wr scss -o css`（开始监听style.scss）
在目录里打开style.scss开始编辑，node-scss就会自动给css目录添加style.css并实时更新css文件。
在 scss 文件里添加
```
@function px( $px ){
  @return $px/$designWidth*10 + rem;
}

$designWidth : 640; // 640 是设计稿的宽度，你要根据设计稿的宽度填写。

.child{
  width: px(320);
  height: px(160);
  margin: px(40) px(40);
  border: 1px solid red;
  float: left;
  font-size: 1.2em;
}
```
在终端：`cat ~/desktop/scss-demo/css/style.css`，可看到变化，scss将px变成了rem放入了css中

