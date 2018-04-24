---
title: webpack入门
date: 2018-04-23 21:00:24
tags:
---
# 1. 初体验
很乱，数不清的配置

# 2. 安装
1. 创建目录
```
mkdir webpack-demo
cd webpack-demo
npm init  //创建一个package.json
```
2. copy [Github上webpack官网](https://github.com/webpack/webpack)的文档
```
//安装webpack
npm install --save-dev webpack  

//配置
touch webpack.config.js
vi  webpack.config.js
//在里面写以下内容
/*
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};*/

//创建文件
touch src/index.js

//运行webpack
npx webpack  //这时会多出dist目录，里面有bundle.js文件
```
3. 在index.js里写
```
console.log(1)

//再运行webpack:
npx webpack

//再看bundle.js，这时会多出来一行console.log(1) 
```

4. 用babel-loader，我用的是 [7.x branch](https://github.com/babel/babel-loader/tree/7.x) for docs with Babel v6
```
//安装v6，命令行
npm install babel-loader babel-core babel-preset-env webpack

//将这个复制到webpack的配置文件webpack.config.js里，加在output的下面
module: {
  rules: [
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }
  ]
}

//加在output的下面，复制完后成这样
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
  rules: [
    {
      test: /\.js$/,
      exclude: /(node_modules|bower_components)/,
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }
  ]
}
};
```
运行`npx webpack`
若出现`can't find '...'`或`can't resolve '...'`的报错，则安装省略号里的东西`npm i '省略号'`
**注意：**若是` Couldn't find preset "env"`，不要安装env，而是`npm i babel-preset-env`

5. 
```
//当你在写index.js里写
let a=1
//它就会帮你自动转换成es5了
```

# 3. 总结
太乱了太多配置了，希望parcel赶快升级替换掉webpack