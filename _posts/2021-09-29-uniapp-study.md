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
