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

## uni-app 异步数据缓存

设置缓存: uni.setStorage(Object)

Object:

- key:本地缓存中的指定的 key String 类型
- data:需要存储的内容
- success:接口调用成功的回调函数
- fail:接口调用失败的回调函数
- complete:接口调用结束的回调函数(调用成功,失败都会执行)

获取缓存: uni.getStorage(Object)

Object:

- key:本地缓存中的指定的 key String 类型
- success:接口调用成功的回调函数

> 成功的数据在返回的 res 里

- fail:接口调用失败的回调函数
- complete:接口调用结束的回调函数(调用成功,失败都会执行)

移除缓存: uni.removeStorage(Object)

- key:本地缓存中指定的 key
- success:接口调用成功的回调函数
- fail:接口调用失败的回调函数
- complete:接口调用结束的回调函数(调用成功,失败都会执行)

## uni-app 同步数据缓存

设置缓存: uni.setStorageSync(key,data))

获取缓存: uni.getStorageSync(key)

移除缓存: uni.removeStorageSync(key)

## uni-app 图片上传和预览

### uni.chooseImage(Object)

从本地相册选择图片或使用相机拍照

<table>
  <thead>
      <tr>
        <th>参数名</th>
        <th>类型</th>
        <th>说明</th>
        <th>差异</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>count</td>
        <td>Number</td>
        <td>最多可以选择图片的数量,默认9</td>
        <td>count 值在 H5 平台的表现，基于浏览器本身的规范。目前测试的结果来看，只能限制单选/多选，并不能限制数量。并且，在实际的手机浏览器很少有能够支持多选的。</td>
      </tr>
      <tr>
        <td>sizeType</td>
        <td>Array<\String>	</td>
        <td>original 原图，compressed 压缩图，默认二者都有</td>
        <td>App、微信小程序、支付宝小程序、百度小程序</td>
      </tr>
      <tr>
        <td>extension</td>
        <td>Array<\String>	</td>
        <td>根据文件拓展名过滤，每一项都不能是空字符串。默认不过滤。</td>
        <td>H5(HBuilder X2.9.9+)</td>
      </tr>
      <tr>
        <td>sourceType</td>
        <td>Array<\String>	</td>
        <td>album 从相册选图，camera 使用相机，默认二者都有。如需直接开相机或直接选相册，请只使用一个选项</td>
        <td></td>
      </tr>
      <tr>
        <td>crop</td>
        <td>Object</td>
        <td>图像裁剪参数，设置后 sizeType 失效</td>
        <td>App 3.1.19+</td>
      </tr>
      <tr>
        <td>success</td>
        <td>Function</td>
        <td>成功则返回图片的本地文件路径列表 tempFilePaths</td>
        <td></td>
      </tr>
      <tr>
        <td>fail</td>
        <td>Function</td>
        <td>接口调用失败的回调函数</td>
        <td>小程序、App</td>
      </tr>
      <tr>
        <td>complete</td>
        <td>Function</td>
        <td>接口调用结束的回调函数（调用成功、失败都会执行）</td>
        <td></td>
      </tr>
  </tbody>
</table>

## uni.previewImage(OBJECT)

图片预览

<table>
    <thead>
      <tr>
        <th>参数名</th>
        <th>类型</th>
        <th>说明</th>
        <th>差异</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>current</td>
        <td>String/Number</td>
        <td>为当前显示图片的链接/索引值，不填或填写的值无效则为 urls 的第一张</td>
        <td>App平台在 1.9.5至1.9.8之间，current为必填。不填会报错</td>
      </tr>
      <tr>
        <td>urls</td>
        <td>Array<\String></td>
        <td>需要预览的图片链接列表</td>
        <td></td>
      </tr>
      <tr>
        <td>indicator</td>
        <td>String</td>
        <td>图片指示器样式，可取值："default" - 底部圆点指示器； "number" - 顶部数字指示器； "none" - 不显示指示器。</td>
        <td>App</td>
      </tr>
      <tr>
        <td>loop</td>
        <td>Boolean</td>
        <td>是否可循环预览，默认值为 false</td>
        <td>App</td>
      </tr>
      <tr>
        <td>longPressActions</td>
        <td>Object</td>
        <td>长按图片显示操作菜单，如不填默认为保存相册</td>
        <td>App 1.9.5+</td>
      </tr>
      <tr>
        <td>success</td>
        <td>Function</td>
        <td>接口调用成功的回调函数</td>
        <td></td>
      </tr>
      <tr>
        <td>fail</td>
        <td>Function</td>
        <td>接口调用失败的回调函数	</td>
        <td></td>
      </tr>
      <tr>
        <td>complete</td>
        <td>Function</td>
        <td>接口调用结束的回调函数（调用成功、失败都会执行）</td>
        <td></td>
      </tr>
  </tbody>
</table>

## 条件注释实现跨段兼容

条件编译使用特殊的注释作为标记,在编译时根据这些特殊的注释,将注释里面的代码编译到不同平台

写法:以 **\#ifdef** 或 **\#inndef** 加 **%PLATFORM** 开头,以**\#endif** 结尾

- #ifdef: if defined 仅在某平台存在
- #inndef: if not defined 除了某平台均存在
- %PLATFORM: 平台名称

<table>
  <thead>
      <tr>
        <th>条件编译写法</th>
        <th>说明</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>
          #ifdef APP-PLUS <br/>
          需要条件编译的代码 <br/>
          #endif
        </td>
        <td>仅出现在 App 平台下的代码</td>
      </tr>
      <tr>
        <td>
          #ifndef H5 <br/>
          需要条件编译的代码 <br/>
          #endif
        </td>
        <td>除了H5平台,其他平台均存在的代码</td>
      </tr>
      <tr>
        <td>
          #ifdef H5 || MP-WEIXIN <br/>
          需要条件编译的代码 <br/>
          #endif
        </td>
        <td>除了H5平台或微信小程序平台存在的代码(这里只有 || ,不可能出现&&,因为没有交集)</td>
      </tr>
  </tbody>
</table>

%PLATFORM% 可取值如下：

<table>
  <thead>
      <tr>
        <th>值</th>
        <th>生效条件</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>VUE3</td>
        <td>HBuilderX 3.2.0+ <a href="https://ask.dcloud.net.cn/article/37834">详情</a> </td>
      </tr>
      <tr>
        <td>APP-PLUS</td>
        <td>App</td>
      </tr>
      <tr>
        <td>APP-PLUS-NVUE或APP-NVUE</td>
        <td>App nvue</td>
      </tr>
      <tr>
        <td>H5</td>
        <td>H5</td>
      </tr>
      <tr>
        <td>MP-WEIXIN</td>
        <td>微信小程序</td>
      </tr>
      <tr>
        <td>MP-ALIPAY</td>
        <td>支付宝小程序</td>
      </tr>
      <tr>
        <td>MP-BAIDU</td>
        <td>百度小程序</td>
      </tr>
      <tr>
        <td>MP-TOUTIAO</td>
        <td>字节跳动小程序</td>
      </tr>
      <tr>
        <td>MP-QQ</td>
        <td>QQ小程序</td>
      </tr>
      <tr>
        <td>MP-KUAISHOU</td>
        <td>快手小程序</td>
      </tr>
      <tr>
        <td>H5</td>
        <td>H5</td>
      </tr>
      <tr>
        <td>MP-360</td>
        <td>360小程序</td>
      </tr>
      <tr>
        <td>MP</td>
        <td>微信小程序/支付宝小程序/百度小程序/字节跳动小程序/QQ小程序/360小程序</td>
      </tr>
      <tr>
        <td>QUICKAPP-WEBVIEW</td>
        <td>快应用通用(包含联盟、华为)</td>
      </tr>
      <tr>
        <td>QUICKAPP-WEBVIEW-UNION</td>
        <td>快应用联盟</td>
      </tr>
      <tr>
        <td>QUICKAPP-WEBVIEW-HUAWEI	</td>
        <td>快应用华为</td>
      </tr>
  </tbody>
</table>

## 路由与跳转 (navigator)

页面跳转 该组件类似 HTML 中的<a>组件,但只能跳转本地页面.目标页面必须在 pages.json 中注册

生命式导航属性说明:

<table>
  <thead>
      <tr>
        <th>属性名</th>
        <th>类型</th>
        <th>默认值</th>
        <th>说明</th>
        <th>平台差异</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>url</td>
        <td>String</td>
        <td></td>
        <td>应用内的跳转链接，值为相对路径或绝对路径</td>
        <td></td>
      </tr>
      <tr>
        <td>open-type</td>
        <td>String</td>
        <td>navigate</td>
        <td>跳转方式. 值有:navigate,redirect,switchTab,reLaunch,navigateBack,exit</td>
        <td></td>
      </tr>
      <tr>
        <td>delta</td>
        <td>Number</td>
        <td></td>
        <td>当 open-type 为 'navigateBack' 时有效，表示回退的层数</td>
        <td></td>
      </tr>
      <tr>
        <td>animation-type</td>
        <td>String</td>
        <td>pop-in/out</td>
        <td>当 open-type 为 navigate、navigateBack 时有效，窗口的显示/关闭动画效果 <a href="https://uniapp.dcloud.io/api/router?id=animation">详情</a></td>
        <td>App</td>
      </tr>
      <tr>
        <td>animation-duration</td>
        <td>Number</td>
        <td>300</td>
        <td>当 open-type 为 navigate、navigateBack 时有效，窗口显示/关闭动画的持续时间。</td>
        <td>App</td>
      </tr>
      <tr>
        <td>hover-class</td>
        <td>String</td>
        <td>navigator-hover</td>
        <td>指定点击时的样式类，当hover-class="none"时，没有点击态效果</td>
        <td></td>
      </tr>
      <tr>
        <td>hover-stop-propagation</td>
        <td>Boolean</td>
        <td>false</td>
        <td>指定是否阻止本节点的祖先节点出现点击态</td>
        <td>微信小程序</td>
      </tr>
      <tr>
        <td>hover-start-time</td>
        <td>Number</td>
        <td>50</td>
        <td>按住后多久出现点击态，单位毫秒</td>
        <td></td>
      </tr>
      <tr>
        <td>hover-stay-time</td>
        <td>Number</td>
        <td>600</td>
        <td>手指松开后点击态保留时间，单位毫秒</td>
        <td></td>
      </tr>
      <tr>
        <td>target</td>
        <td>String</td>
        <td>self</td>
        <td>在哪个小程序目标上发生跳转，默认当前小程序，值域self/miniProgram</td>
        <td></td>
      </tr>
  </tbody>
</table>

### 示例

{% highlight js linenos %}
<navigator url="navigate/navigate?title=navigate" hover-class="navigator-hover">
<button type="default">跳转到新页面</button>
</navigator>
{% endhighlight %}

编程式导航:

- uni.navigateTo(OBJECT)

  OBJECT 参数说明

  - url: String 类型, 必填, 需要跳转的应用内非 tabBar 的页面的路径 , 路径后可以带参数。参数与路径之间使用?分隔，参数键与参数值用=相连，不同参数用&分隔；如 'path?key=value&key2=value2'，path 为下一个页面的路径，下一个页面的 onLoad 函数可得到传递的参数
  - animationType: String 类型, 非必填, 默认值:pop-in, 窗口显示的动画效果 <a href="https://uniapp.dcloud.io/api/router?id=animation">详情</a> 仅支持 APP
  - animationDuration: Number 类型, 非必填, 默认值:300, 窗口动画持续时间，单位为 ms 仅支持 APP
  - events: Object 类型, 非必填, 页面间通信接口，用于监听被打开页面发送到当前页面的数据。2.8.9+ 开始支持。
  - success: 成功回调
  - fail: 失败回调
  - complete: 接口调用结束的回调

- uni.redirectTo(OBJECT)

  会销毁当前页面

## uni-app 组件

组件的生命周期同 vue 2.0

### 组件的通讯

父->子: 在父组件中给子组件绑定属性,在子组件中通过 props 接收 (同 vue)

子->父: 通过\$emit 来触发事件 (同 vue)

兄弟组件之间传值: uni.on() 注册全局监听的事件 uni.\$emit() 触发全局的监听事件

## uni-ui 的使用

<a href="https://uniapp.dcloud.io/component/README?id=uniui">地址</a>

## 封装 uni.request 请求

{% highlight js linenos %}
const BASE_URL = 'xxxxxxxxxxxx'
export const myRequest = (options)=>{
return new Promise((resolve,reject)=>{
uni.request({
url:BASE_URL+options.url,
method: options.method || 'GET',
data:options.data || {},
success: (res) => {
if(res.data.status !== 0){
return uni.showToast({
title:'获取数据失败'
})
}
resolve(res)
},
fail: (err) => {
uni.showToast({
title:'请求接口失败'
})
reject(err)
}
})
})
}
{% endhighlight %}

在 main.js 中导入

- import {myRequest} from './pages/util/api.js'

- Vue.prototype.\$myRequest = myRequest

## 小程序的发布

在 manifest.js 页面的 微信小程序配置中 配置 AppID 在微信开发者工具中点击上传即可

### 微信小程序发布线上地址

1. 需要线上的接口地址 在代码中将请求换成线上的地址

2. 将线上地址的接口域名配置到 小程序的服务器域名

3. 发布上线的时候需要将字体图标放到线上的服务器中

## h5 的发布

在 manifest.js 页面的 h5 配置中 配置 项目名称 路由方式 等

点击 发行-> 网站-H5 手机版

## App 的发布

1. 在基础配置中 uni-app 应用标识 (没有的需要 重新获取)

2. APP 图标配置

3. App 启动图配置

4. App SDK 配置 (用到哪些钩哪些)

5. App 模块权限配置 (用到哪些钩哪些)

6. App 原生插件配置

7. App 常用其他配置

8. 点击发行 -> App 云打包 (生成安卓, IOS 包,在公司 使用自有证书)
