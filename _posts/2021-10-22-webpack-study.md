---
layout: post
title: Webpack Study
tags: mathjax
math: true
date: 2021-10-21 12:00 +0800
---

学习 Webpack 的历程
{: .message }

## Webpack 介绍

<a href="https://webpack.docschina.org/">地址</a>

Webpack 是一种前端资源构建工具(不能直接解析 less,等),一个静态模块打包器(module bundler).

在 Webpack 看来,前端的所有资源文件(js/json/css/img/less/...)都会作为模块处理.

它将根据模块的依赖关系进行静态分析,打包生成对应的静态资源(bundle)

- 静态模块打包器:根据入口文件的依赖关系,将资源全部引进来,生成 chunk(代码块),然后根据 chunk 根据不同的资源进行不同的处理,进行打包,输出出去的文件叫 bundle

## Webpack 五个核心概念

### Entry

入口(Entry) 指示 Webpack 以那个文件为入口为入口起点开始打包,分析构建内部依赖图

### Output

输出(Output) 指示 Webpack 打包后的资源 bundles 输出到哪里去,以及如何命名

### Loader

Loader 让 Webpack 能够去处理那些非 JaceScript 文件 (webpack 自身只理解 JavaScript,将 css,img 翻译成 js)

### Plugins

插件(Plugins) 可以用于执行范围更广的任务,插件的范围包括,从打包优化和压缩,一直到重新定义环境中的变量等

### Mode

模式(Mode) 指示 Webpack 使用相应模式的配置

## 初体验

创建 build 文件夹, 创建 src 文件夹,在里面创建 index.js 文件

index.js 作为 webpack 入口起点文件

### 运行指令

开发环境:

- webpack ./src/index.js -o ./build/built.js --mode=development
- webpack 会以 ./src/index.js 为入口文件开始打包,打包后输出到 ./build/built.js
- 整体打包环境,是开发环境

生产环境:

- webpack ./src/index.js -o ./build/built.js --mode=production
- webpack 会以 ./src/index.js 为入口文件开始打包,打包后输出到 ./build/built.js
- 整体打包环境,是生产环境

### 结论

- webpack 能处理 js/json 文件,不能处理 css/img 等其他资源
- 生产环境和开发环境将 ES6 模块化编译成浏览器能识别的模块化
- 生产环境比开发环境多一个压缩 js 代码

## 打包样式资源

1. 和 src 同级 创建 webpack.config.js 打包压缩 css 和 img 资源

- - 指示 webpack 做什么 (当运行的时候 webpack 指令时,会加载里面的配置)

**所有的构建工具都是基于 node 平台运行的 模块化默认采用 common.js**

### 开发环境配置

运行项目指令

- webpack 会将打包结果输出出去
- npx webpack-dev-server 只会在内存中编译打包, 没有输出

{% highlight js linenos %}
const {resolve} = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
// 打包 css 成一个单独的文件的插件
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
// 压缩 css
const OptimizeCssAssetsWebpackPlugin = require('optimize-css-assets-webpack-plugin')

// 设置 nodejs 环境变量
process.env.NODE_ENV = 'development';

module.exports = {
//webpack 配置
//入口文件
entry:'./src/index.js',
//输出
output:{
//输出文件名
filename:'js/built.js',
//输出路径
// \_\_dirname node.js 的变量,代表当前文件的目录绝对路径
path:resolve(\_\_dirname,'build')
},

<!-- loader的配置 -->

module:{
rules:[
// 详细的 loader 配置
// 不同文件必须配置不同 loader 处理
{
// 匹配哪些文件
test:/\.css\$/,
//使用哪些 loader 进行处理
use:[
// use 数组中 loader 执行顺序,从右到左,从下到上,依次执行
// 创建 style 标签,将 js 中的样式资源插入进去,添加到 head 中生效

<!-- 'style-loader', -->

这个 loader 取代 style-loader.作用:提取 js 中的 css 成单独文件
MiniCssExtractPlugin.loader,
// 将 css 文件变成 common.js 模块加载到 js 中,里面内容是样式字符串
'css-loader',

// css 兼容性处理: postcss -- > postcss-loader postcss-preset-env
// 帮 postcss 找到 package.json 中 browserslist 里面的配置,通过配置加载指定的 css 兼容性样式

// 使用 loader 的默认配置
// 'postcss-loader',
// 修改 loader 的配置
{
loader:'postcss-loader',
options:{
ident:'postcss',
plugins:()=>[
// postcss 的插件
require('postcss-preset-env')()
]
}
}
]
},
{
test:/\.less&/,
use:[
'style-loader',
'css-loader',
// 需要下载 less-loader less
'less-loader'
]
},
{
// 处理图片
// 默认处理不累 html 中 img 图片
test:/\.(jpg|png|gif)\$/,
// 下载 url-loader file-loader
loader:'url-loader',
options:{
//图片大小小于 8kb,就会被 base64 处理
//优点:减少请求数量(减轻服务器压力)
//缺点:图片体积会更大(文件请求速度更慢)
limit:8\*1024
// 问题:因为 url-loader 默认使用 es6 模块化解析,而 html-loader 引入图片是 commonjs
// 解析时会出问题: [object Module]
// 解决:关闭 url-loader 的 es6 模块化,使用 commonjs 解析
esModule:false,
outputPath:'imgs',
//给图片进行重命名
//[hash:10] 取图片的 hash 原来的前 10 位
//[ext]取文件拓展名
name:'[hash:10].[ext]'
}
},
{
test:/\.html\$/,
// 处理 html 文件的 img 图片(负责引入 img,从而能被 url-loader 进行处理)
loader:'html-loader'
}
// 打包其他资源
{
// 排除 css/js/html 资源
exclude:'/\.(css|js|html|less)\$/,
loader:'file-loader',
options:{
name:'[hash:10].[ext]',
outputPath:'media',
}
}
]
},
// plugins 的配置
plugins:[
// 详细 plugins 的配置

// 下载插件 html-webpack-plugin
// 功能: 默认会创建一个空的 html,自动引入打包输出的所有资源(JS/CSS)
// 需求:需要有结构的 HTML 文件
new HtmlWebpackPlugin(
{
// 复制'./src/index.html' 文件,并自动引入打包输出的所有资源(JS/CSS)
template:'./src/index.html,
minify:{
// 移除空格
collapseWhitespace:true,
// 移除注释
removeComments:true
}
}
)

new MiniCssExtractPlugin({
// 对输出的 css 文件进行重命名
filename:'css/built.css'
})

// 压缩 css optimize-css-assets-webpack-plugin
new OptimizeCssAssetsWebpackPlugin()
],
// 模式
mode:'development', // 开发模式

<!-- mode:'production'  -->

// 开发服务器 devServer:用来自动化 (自动编译,自动打开浏览器,自动刷新浏览器)
// 特点: 只会在内存中编译打包,不会有任何输出
// 启动 devServer 指令为: npx webpack-dev-server (需要下载 webpack-dev-server)
devServer:{
// 项目构建后的路径
contentBase:resolve(\_\_dirname,'build'),
// 启动 gzip 压缩
compress:true,
// 端口号
port:3000,
// 自动打开浏览器
open:true
}
}
{% endhighlight %}

- package.json 中 browserslist 里面的配置

  {% highlight js linenos %}
  "browserslist":{
  // 开发环境 --> 设置 node 环境变量:process.env.NODE_ENV = development
  "development":[
  "last 1 chrome version", // 兼容最近的一个 chrome 版本
  "last 1 firefox version", // 兼容最近的一个 firefox 版本
  "last 1 safari version", // 兼容最近的一个 safari 版本
  ],
  // 生产环境: 默认是看生产环境
  "production":[
  ">0.2%",
  "not dead",
  "not op_mini all"
  ]
  }
  {% endhighlight %}

## JS 的语法检查

- 语法检查: eslint-loader eslint
- 注意: 只检查自己写的源代码,第三方的库是不用检查的
- 设置检查规则 :
  - package.json 中 eslintConfig 中设置
  - airbnb --> eslint-config-airbnb-base eslint eslint-plugin-import

{% highlight js linenos %}
{
test:/\.js\$/,
exclude:/node-modules/,
loader:'eslint-loader',
// 优先执行
enforce:'pre',
options:{
fix:true
}
}
{% endhighlight %}

- package.json 中 eslintConfig 里面的配置 eslint

  {% highlight js linenos %}
  "eslintConfig":{
  "extends":"airbnb-base"
  }
  {% endhighlight %}

  - // 下一行 eslint 所有规则都失效(下一行不进行 eslint 检查)
  - // eslint-disable-next-line

## js 的兼容性处理

- babel-loader @babel/preset-env @babel/core
- 全部 js 兼容性处理: @babel/polyfill
- 需要兼容性处理的就做: 按需加载 -->core-js
  {% highlight js linenos %}
  {
  test:/\.js\$/,
  exclude:/node-modules/,
  loader:'babel-loader',
  options:{
  presets:[
  [
  '@babel/preset-env',
  {
  useBuiltIns:'usage',
  corejs:{
  version:3
  },
  // 指定兼容性做到哪个版本浏览器
  targets:{
  chrome:'60',
  firefox:'60',
  ie:'9',
  safari:'10',
  edge:'17'
  }
  }
  ]
  ]
  }
  }
  {% endhighlight %}

## js 的压缩

- mode:production 时会自动进行压缩

# Webpack 性能优化介绍

- 开发环境性能优化
- 生产环境性能优化

## 开发环境性能优化 : 速度快,调试更友好

速度快:(eval>line>cheap>...)

eval-cheap-source-map

eval-source-map

调试更友好:source-map

cheap-module-source-map

cheap-source-map

--> eval-source-map / eval-cheap-module-source-map

- 优化打包构建速度

  /\*

  HMR : hot module replacement 热模块替换 / 模块热替换

  作用:一个模块发生变化,只会重新打包这一个模块(而不是打包所有魔模块)

  极大提升构建速度

  样式文件:可以使用 HMR 功能:因为 style-loader 内部实现了

  js 文件:默认不能使用 HMR 功能 --> 需要修改 js 代码,添加支持 HMR 功能的代码

  - 注意:HMR 功能对 js 的处理,只能处理非入口 js 文件的其他文件.

  html 文件:默认不能使用 HMR 功能,同时会导致 html 文件不能热更新了(不用做 HMR 功能)

  - 解决:修改 entry 入口,将 html 文件引入

  \*/
  {% highlight js linenos %}
  devServer:{
  // 开启 HMR 功能
  // 当修改了 webpack 配置,新配置要想生效,必须要重新 webpack 服务
  hot:true
  }
  {% endhighlight %}

- 优化代码调试

  source-map : 一种提供源代码到构建后代码映射 技术(如果构建代码出错,通过映射可以追踪代码错误)
  {% highlight js linenos %}
  devServer:{
  ...
  },
  devtool:'source-map'
  /**
  source-map:外部 错误代码准确信息 和 源代码的错误位置
  inline-source-map:内联 1.只生成一个内联 source-map 2.错误代码准确信息 和 源代码的错误位置
  hidden-source-map:外部 1.错误代码的错误原因, 但是没有错误位置 不能追踪到源代码, 只能提示到构建后代码的错误位置
  eval-source-map:内联 1.每一个文件都生成对应的 source-map, 都在 eval 中 2.错误代码准确信息 和 源代码的错误位置
  nosurces-source-map:外部 1.错误代码准确信息, 但是没有任何源代码信息
  cheap-source-map:外部 1.错误代码准确信息 和 源代码的错误位置, 只能精确到行
  cheap-module-source-map:外部 1.错误代码准确信息 和 源代码的错误位置
  内联 和 外部 的区别: 1.外部生成了文件,内联没有 2. 内联构建速度更快
  **/
  {% endhighlight %}

## 生产环境性能优化 : 源代码要不要隐藏? 调试要不要更友好

内联会让代码体积更大,所以在生产环境不同内联

代码隐藏: nosurces-source-map 全部隐藏

hidden-source-map 只隐藏源代码,会提示构建后代码错误信息

调试友好: source-map

--> source-map / cheap-module-source-map

- 优化打包构建速度
- 优化代码运行的性能

## oneOf

在 rules 里用 oneOf 数组包裹

// 以下 loader 只会匹配一个

// 注意: 不能有两个配置处理同一种类型文件 (同一个要提取出去)

## 缓存

- babel 缓存: cacheDirectory:true
- 文件资源 缓存: hash: 每次 webpack 构建时会发生一个唯一的 hash 值
  - 问题: 因为 js 和 css 同时使用一个 hash 值,如果重新打包,会导致所有缓存失效.(可能只改动一个文件)
  - chunkhash: 根据 chunk 生成的值.如果打包来源于同一个 chunk,那么 hash 值就一样
    - 问题: js 和 css 的 hash 还是一样的? 因为 css 是在 js 中被引入的,所以同属于一个 chunk
  - contenthash: 根据文件的内容生成 hash 值,不同文件 hash 值一定不一样
    - --> 让代码上线运行缓存更好使用

## tree shaking

目的:去除无用代码

前提:

- 1. 必须使用 ES6 模块化
- 2. 开启 production 环境
  - 作用:减少代码体积
- 3. 在 package.json 中配置 "sideEffects":false 所有代码都没有副作用(都可以进行 tree shaking)
  - 问题: 可能会把 css / @babel/polyfill (副作用)文件干掉
  - "sideEffects":["*.css","*.less"]

# code split 代码分割

- 单入口:entry:'./src/js/index/js',
- 多入口:
  - index:'./src/js/index/js',
  - test:'./src/js/test.js'
- 可以将 node_modules 中代码单独打包一个 chunk 最终输出. 自动分析多入口 chunk 中,有没有公共的文件.如果有会打包成单独的一个 chunk
  {% highlight js linenos %}
  optimization:{
  splitChunks:{
  chunks:'all'
  }
  }
  {% endhighlight %}

- 通过 js 代码,让某个文件单独打包成一个 chunk. import 动态导入语法,能将某个文件单独打包
  {% highlight js linenos %}
  import(/\* webpackChunkName: 'test' \*/'./test')
  .then((res) =>{
  ...
  })
  .catch(()=>{
  //eslint-disable-next-line
  console.log('文件加载失败')
  })
  {% endhighlight %}

## 懒加载和预加载

{% highlight js linenos %}
// 在需要进行懒加载的地方使用: 当文件使用时才加载
// webpackPrefetch: 预加载: 会在使用之前,提前加载 js 文件
// 正常加载是并行加载(同一时间加载多个文件) 预加载 等其他资源加载完毕,再偷偷加载资源
import(/\* webpackChunkName: 'test',webpackPrefetch: true \*/'./test')
.then(({mul})=>{
...
})
{% endhighlight %}

## PWA 渐进式网络开发应用程序(离线可访问)

workbox --> workbox-webpack-plugin

import WorkboxWebpackPlugin = require('workbox-webpack-plugin')

{% highlight js linenos %}
在 plugins:[
new WorkboxWebpackPlugin.GenerateSW({
// 帮助 serviceworker 快速启动
// 删除旧的 serviceworker

// 生成 serviceworker 配置文件
clientsClaim:true,
skipWaiting:true
})
]
{% endhighlight %}

/ \*\*

1. eslint 不认识 window,navigator 全局变量
   解决:需要修改 package.json 中 eslintConfig 配置
   "env":{
   "browser":true // 支持浏览器端全局变量
   }
2. sw 代码必须训醒在服务器上
   -->nodejs
   -->
   node i serve -g
   serve -s build 启动服务器,将 build 目录下所有资源作为静态资源暴露出去

\*\* /

// 注册 serviceWorker
// 处理兼容性问题
{% highlight js linenos %}
if('serviceWorker' in navigator){
window.addEventListener('load',()=>{
navigator.serviceWorker.register('/service-worker.js')
.then(()=>{
console.log('sw 注册成功了')
})
.catch(()=>{
console.log('sw 注册失败了')
})
})
}
{% endhighlight %}

## 多进程打包

npm i thread-loader -D

{% highlight js linenos %}
use:[
// 开启多进程打包
// 进程启动大概为 600ms,进程通信也有开销,
// 只有工作消耗时间比较长,才需要多进程打包
'thread-loader',
{
loader:'babel-loader',
...
}
]
{% endhighlight %}

## externals

和 mode 同级
{% highlight js linenos %}
externals:{
// 拒绝被打包进去
jquery:'jQuery'
}
{% endhighlight %}
需要手动在 index.js 中引入 cdn 中的包

## dll

// 使用 dll 技术对某些库(第三方的库:jquery,react,vue)进行单独打包
// 当运行 webpack 时,默认查找 webpack.config.js 配置文件
需求
{% highlight js linenos %}
const {resolve} = require('path')
module.exports={
entry:{
// 最终打包生成的[name] -->jquery
// ['jquery'] --> 要打包的库是 jquery
jquery:['jquery']
},
output:{
fillname:'[name].js',
path:resolve(\_\_dirname,'dll'),
library:'[name]\_[hash]',// 打包的库里面向外暴露出去的内容叫什么名字
plugins:[
// 打包生成一个 mainfest.json -->提供和 jquery 映射
new webpack.DllPlugin({
name:'[name]\_[hash]', // 映射库的暴露的内容名称
path:resolve(\_\_dirname,'dll/mainfest.json') // 输出文件路径名称
})
],
mode:'production'
}
}
{% endhighlight %}

## optimization

{% highlight js linenos %}
const TerserWebpackPlugin = require('terser-webpack-plugin')
// 将当前模块的记录其他模块的 hash 单独打包为一个文件 runtime
// 解决:修改 a 文件导致 b 文件的 contenthash 变化
optimization:{
splitChunks:{},
runtimeChunk:{
name:entrypoint =>`runtime - ${entrypoint.name}`
},
minimizer:{
// 配置生产环境的压缩方案:js 和 css
new TerserWebpackPlugin({
// 开启缓存
cache:true,
// 开启多进程打包
parallel:true,
// 启动 source-map
sourceMap:true
})
}
}
{% endhighlight %}
