---
layout: post
title: Uniapp Study
tags: mathjax
math: true
date: 2021-09-29 12:00 +0800
---

学习 UniApp 的历程
{: .message }

## uni-app 介绍

uni-app 是一个使用 Vue.js 开发所有前端应用的框架,开发者便携一套代码,可以发不到 iOS,安卓,H5,以及各个小程序等多个平台.

> 具有 vue 和微信小程序的开发经验,可快速上手 uni-app

## 环境搭建

- 1.安装编辑器 Hbuilderx <a href="https://www.dcloud.io/hbuilderx.html">下载地址</a>
- 2.安装微信开发者工具 <a href='https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html'>下载地址</a>

## 运行微信开发者工具模拟器

- 1.如果是第一次使用，需要先配置小程序 ide 的相关路径，才能运行成功。如下图，需在输入框输入微信开发者工具的安装路径。 若 HBuilderX 不能正常启动微信开发者工具，需要开发者手动启动，然后将 uni-app 生成小程序工程的路径拷贝到微信开发者工具里面，在 HBuilderX 里面开发，在微信开发者工具里面就可看到实时的效果。
  ![alt](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/a142b6a0-4f1a-11eb-8a36-ebb87efcf8c0.png)
- 2.微信小程序的 **设置 --> 安全 --> 服务窗口 开启** 不开启会报错

## 运行到手机模拟器

- 1.手机数据线和电脑连接,下载包

## 为了实现多端兼容,综合考虑编译速度,uni-app 约定了如下开发规范

- 1.页面文件遵循 **Vue 单文件组建(SFC)规范**
- 2.组件标签靠近小程序规范
- 3.接口能力(JS API)靠近微信小程序规范,但需要将前缀 **wx** 替换成 **uni**
- 4.数据绑定及事件处理同 **Vue.js** 规范,同时补充了 App 及页面的生命周期
- 5.为兼容多端运行,建议使用 **flex 布局** 进行开发

## uni-app 全局配置

- 1.在文件**_pages.json_**
  <table>
    <thead>
      <tr>
        <th>属性</th>
        <th>类型</th>
        <th>默认值</th>
        <th>描述</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>navigationBarBackgroundColor</td>
        <td>HexColor</td>
        <td>#F7F7F7</td>
        <td>导航栏背景颜色</td>
      </tr>
      <tr>
        <td>navigationBarTextStyle</td>
        <td>String</td>
        <td>white</td>
        <td>导航栏标题颜色及状态栏前景颜色 仅支持black/white</td>
      </tr>
      <tr>
        <td>navigationBarTitleText</td>
        <td>String</td>
        <td></td>
        <td>导航栏标题文字内容</td>
      </tr>
      <tr>
        <td>backgroundColor</td>
        <td>HexColor</td>
        <td>#ffffff</td>
        <td>窗口背景颜色(需要在微信开发者工具中查看)</td>
      </tr>
      <tr>
        <td>backgroundTextStyle</td>
        <td>String</td>
        <td>dark</td>
        <td>下拉loading的样式,仅支持dark/light</td>
      </tr>
      <tr>
        <td>onReachBottomDistance</td>
        <td>Number</td>
        <td>50</td>
        <td>页面上拉触底事件触发时距页面底部距离,单位只支持px(距离底部多少的时候,加载下一页的数据)</td>
      </tr>
    </tbody>
  </table>

## 通过 pages 来配置页面

> pages 的第一个对象就是初始页面

> pages 的内部样式会覆盖全局样式

<table>
  <thead>
      <tr>
        <th>属性</th>
        <th>类型</th>
        <th>默认值</th>
        <th>描述</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>path</td>
        <td>String</td>
        <td></td>
        <td>配置页面路径</td>
      </tr>
      <tr>
        <td>style</td>
        <td>Object</td>
        <td></td>
        <td>配置页面窗口表现</td>
      </tr>
  </tbody>
</table>

> 在 pages 中,可以给 h5 或者 app-plus 单独设置样式

## 配置 tabbar (<a href='https://uniapp.dcloud.io/collocation/pages?id=tabbar'>详情</a>)

<abbr>如果应用是一个多 tab 应用,可以通过 tabBar 配置项指定 tab 栏的表现,以及 tab 切换时小时的对应项<abbr>

### Tips

- 1.当设置 position 为 top 时,将不会显示 icon (浏览器中不可以,只能在小程序中)
- 2.tabBar 中的 list 是一个数组,只能配置最少 2 个,最多 5 个 tab,tab 按数组的顺序排序

### 通过 condition 配置微信小程序详情页的启动模式

# 组件的基本使用

## text 文本组件 (行内元素)

属性:

- selectable :控制文本是否可选 默认 false
- space :显示连续空格,可选参数:ensp,emsp,nbsp
- decode :默认解码

## view 组件 容器组件 (相当于 html 中的 div)

属性:

- hover-class :指定按下去的样式类
- hover-stop-propagation :是否阻止本节点的祖先节点出现点击状态 (类似于阻止冒泡的效果)
- hover-start-time :按住后多久出现点击状态 单位毫秒 默认值:50
- hover-stay-time :手指松开后点击状态保留时间 单位毫秒

## button 组件

属性

- size
- type :primary default warn
- plain :镂空
- disabled :禁用
- loading : loading 效果

## image 组件 图片组件

属性

- src 图片资源路径
- mode :
  > aspectFit 保持纵横比缩放图片,使图片的长边完全显示出来
  > aspectFill 保持纵横比缩放图片,使图片的短边完全显示出来

## uni-app 中的样式

- 1.rpx 即响应式 px,一种根据屏幕宽度自适应的动态单位,以 750 宽的屏幕为基准,750rpx 恰好为屏幕宽度,屏幕变宽,rpx 实际显示效果会等比放大.
- 2.使用 **_@import_** 语句可以倒入外链样式表
- 3.在 uni-app 中可以使用基本的选择器
- 4.在 uni-app 中不能使用 **\*** 选择器
- 5.**_page_**相当于**_body_**节点
- 6.在 App.vue 中的样式为全局样式,作用于每一个页面,在 pages 目录下的 vue 文件中定义的样式为局部样式,只作用在对用的页面,会覆盖 App,vue 中相同的选择器
- 7.在 uni-app 中使用字体图标,使用方式和普通的 web 项目相同,需要注意:

  > 字体文件小于 40kb,uni-app 会自动将其转化为 base64 格式

  > 字体文件大于 40kb,需开发者自己转换,否则使用将不生效

  > 字体文件的引用路径推荐使用以 **_-@_** 开头的绝对路径 (src:url('-@/static/....'))

## uni-app 数据绑定 和 Vue 的数据绑定相同

> 在点击事件中传递事件对象,在方法中传入 \$event

## uni-app 中的生命生命周期

- 应用的声明周期:

  onLaunch: 全局只会触发一次

  onShow:从后台进入前台显示

  onHide:从前台进入后台

  onError:报错时触发

- 页面的生命周期:

  onLoad:监听页面加载,其参数为上个页面传递的数据,参数类型为 Object

  onShow:监听页面显示,页面每次出现在屏幕上都触发,包括从下级页面返回

  onReady:监听页面初次渲染完成

  onHide:监听页面隐藏

  onUnload:监听页面卸载

  onPullDownRefresh:监听用户下拉动作，一般用于下拉刷新

  onReachBottom:页面滚动到底部的事件（不是 scroll-view 滚到底），常用于下拉下一页数据。具体见下方注意事项

## uni-app 发送网络请求

> uni.request(Object)

#### Object:

- url: 开发者服务器接口地址 String 类型
- data: 请求的参数 Object/String/ArraryBuffer
- header: 设置请求的 header,header 中不能设置 Referer Object 类型
- method: 请求的方法 String 类型 默认 GET
- timeout: 超市时间,单位是 ms Number 类型
- dataType: 如果设为 json,会尝试对返回的数据做一次 JSON.parse String 类型
- success: 成功之后返回的回调函数

## uni-app 数据缓存

设置缓存: uni.setStorage(Object)

Object:

- key:本地缓存中的指定的 key String 类型
- data:需要存储的内容
- success:接口调用成功的回调函数
- fail:接口调用失败的回调函数
- complete:接口调用结束的回调函数(调用成功,失败都会执行)
