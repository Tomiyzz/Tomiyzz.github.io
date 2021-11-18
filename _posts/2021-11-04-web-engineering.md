---
layout: post
title: 前端工程化
tags: mathjax
math: true
date: 2021-11-02 12:00 +0800
---

学习 前端工程化 的历程
{: .message }

## 前端工程化是什么?

- 前端工程化就是通过各种工具和技术,提升前端开发效率的过程

  (1.项目上线前,代码需要压缩 2.想要使用 ES6+或 CSS3 新特性,要解决兼容性问题 3.想要使用 Less 增强 Css 的编程性,但是浏览器不能直接支持 Less 4.多人协作开发)

  - 前端工程化的内容:各种工具和技术
  - 前端工程化的作用:通过使用工具,提升开发效率

一个工程的生命周期

- 工程立项->需求分析->产品原型->开发实施->测试部署->上线运行

## 前端工程还包括的内容

- 脚手架工具: 1. 专用脚手架 (vue-cli, create-react-app, angular-cli, gatsby-cli) 2. 通用脚手架 (Yeoman, Plop)
- 自动化构建: npm script & script hooks Grunt, Gulp, FIS
- 模块化打包: Webpack, Rollup, Parcel
- 标准化规范: ESLint, StyleLint, Prettier
- 自动化测试: Mocha, Jest, Enzyme, Cypress, Nightmare, Puppeteer
- 自动化部署: Git Hook, Lint-staged, CI/CD

## Yeoman 的基本概念

- Yeoman 是一款脚手架工具
  - 可以帮助开发人员创建项目的基础结构代码
- yo 是 Yeoman 的命令行管理工具
  - 可以在命令行运行 Yeoman 的命令
- 生成器: Yeoman 中具体的脚手架
  - 正对不同项目有不同的脚手架(例如:网站,APP,小程序等)
