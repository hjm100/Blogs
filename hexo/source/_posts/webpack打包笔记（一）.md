---
title: webpack打包笔记（一）
date: 2017-11-24 11:19:07
author: 鸿基梦
categories: web
tags: webpack打包
---

# webpack打包笔记（一）（相关概念总结）：

## 1.基本概念理解：
webpack打包文件命名：webpack.config.js
### 入口  （entry）

入口告诉webpack工作的起点（你要告诉webpack从那个文件开始，进入入口起点后webpack会逐步打包与之有关联的文件）

简单例子：
``` bash

const config = {
  entry:'./main.js' //打包的入口文件是main.js
}

module.exports = config;

//向entry传入一个数组时，将创建多个主入口
entry:['./entry1','./entry2']
``` 
### 深入入口

用法：entry: string|Array<string>

对象语法：(可以根据键值使用：常用于多页面)
用法：entry: {[entryChunkName: string]: string|Array<string>}

用例：
```bash
//分离 应用程序(app) 和 第三方库(vendor) 入口
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};

//这两个依赖图是完全分离的，相互独立的，这种方式常用于只有一个入口文件的单页应用中

```

多页面应用程序

```bash

const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};

```
这是三个独立分离的依赖图

根据经验：每个 HTML 文档只使用一个入口起点。

### 输出  （output）

出口告诉webpack在哪里输出打包的内容，以及如何命名这些打包的文件，你可以通过在配置中指定一个output字段来配置处理过程

简单例子：

```bash

//path模块是路径的兼容写法（兼容windows 与linux）
const path = require('path')
const config = {
    entry:'./main.js' //打包的入口文件是main.js
    output:{
        path:path.resolve(__dirname,'dist'),  //目标输出目录 path 的绝对路径。
        filename:'bundle.js'                  //用于输出文件的文件名。
    }
};

//此配置将一个单独的 bundle.js 文件输出到 /home/proj/public/assets 目录中

module.exports = config;

//上面例子我们通过output.path与output.filename来告诉webpack 打包的名称
//以及我们想要将文件打包到哪里去

```
### 深入输出

多个入口起点
```bash
  output: {
    filename: '[name].js', //自动匹配
    path: __dirname + '/dist'

  }
```

### 加载器（loader）

加载器告诉webpack去处理那些非js文件，（webpack只理解js）,loader能够将有类型的文件转换成webpack能够处理的有效模块。

loader有两个目标

1.识别出应该被对应的loader转化的那些文件（test属性）

2.转换这些文件，使其能够添加到依赖图中

```bash

const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' } //使用 raw-loader模块处理txt文件
      {
        test: /\.css$/,   
        use: [
          { loader: 'style-loader' }, //对 .css 文件使用 style-loader 和 css-loader
          {
            loader: 'css-loader',
            options: {               //启动/禁用 CSS 模块
              modules: true
            }
          }
        ]
      }
    ]
  }
};

// /\.txt$/正则表达式:匹配以 .txt 结尾的文件

module.exports = config;

//解析：当webpack碰到.txt路径的时候，在打包之前先使用raw-loader转换一下
//注意：在配置loader的时候需要定义在module.rules中，而不是rules中，
//定义出错的时候webpack会给出严重的警告

```
### 深入加载器

loader 可以使你在 import 或"加载"模块时预处理文件

使用加载器的时候往往伴随着安装npm包

```bash
常见的加载器 (使用的时候可以去webpack官网寻找自己想要使用的模块即可)：

npm install --save-dev css-loader //加载 CSS 文件
npm install --save-dev ts-loader //将 TypeScript 转为 JavaScript
npm install --save-dev raw-loader //加载 txt 文件

更多的加载器不一一赘述
vue-loader   //转换vue文件
html-loader  //加载html（一般需要配合file-loader或url-loader）使用
babel-loader //允许使用Babel和webpack来转换JavaScript文件。
url-loader   //加载文件作为base64编码的URL
file-loader  //生成的文件的文件名就是文件内容的 MD5 哈希值并会保留所引用资源的原始扩展名。

```

module.rules 允许你在 webpack 配置中指定多个 loader。

### 插件  （plugins）

插件告诉webpack可以用于执行范围广的任务，从打包到优化一直到重新定义环境变量，

插件能够处理各种各样的任务

插件定义在 plugins数组中通过New操作符来创建一个插件实例

```bash

const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件
const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;

```
### 配置

 webpack 配置是标准的 Node.js CommonJS 模块，你可以做到以下事情：

1 通过 require(...) 导入其他文件

2 通过 require(...) 使用 npm 的工具函数

3 使用 JavaScript 控制流表达式，例如 ?: 操作符

4 对常用值使用常量或变量

5 编写并执行函数来生成部分配置

###模块

对比 Node.js 模块，webpack 模块能够以各种方式表达它们的依赖关系

1 ES2015 import 语句

2 CommonJS require() 语句

3 AMD define 和 require 语句

4 css/sass/less 文件中的 @import 语句。

5 样式(url(...))或 HTML 文件(<img src=>)中的图片链接(image url)

webpack 提供了可定制的、强大和丰富的 API，可以自己编写加载器等

模块化编程：是开发，测试生成互不影响


###依赖图

任何情况下，一个文件依赖另一个文件，我们把这种依赖关系称作为依赖图谱

### 构建目标(Targets)

在webpack 配置中设置 target 的值。

可以指定是基于什么环境开发的(默认为web)

配置多个targent

```bash

var path = require('path');
var serverConfig = {
  target: 'node',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.node.js'
  }
  //…
};

var clientConfig = {
  target: 'web', // <=== 默认是 'web'，可省略
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'lib.js'
  }
  //…
};

module.exports = [ serverConfig, clientConfig ];

```

# 持续更新中（错误指正，新概念补充）

## 参考来源：https://doc.webpack-china.org/

## webpack打包笔记（二）（实战练习）