---
title: 前端性能优化
date: 2022-03-01 05:08:08
author: cookie
img: ../images/24.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/24.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: 前端性能优化
categories: 性能
tags:
  - 性能优化
---

## 性能优化是什么

从前端的角度来说，性能优化可以分为两个方向。从用户角度来看，一个是页面加载的很快，另一个是页面使用起来很流畅。因此，对性能优化的探索，我们可以分为页面加载时间跟页面运行效率两个方向来进行研究。

## 思想优化

### 1、减少 HTTP 请求

一个完整的 HTTP 请求需要经历 DNS 查找，TCP 握手，浏览器发出 HTTP 请求，服务器接收请求，服务器处理请求并发回响应，浏览器接收响应等过程。所以对于一些可以存放在本地的资源，没有必要通过 http 请求去获取。

### 2、使用 HTTP2

相对于 HTTP1.1 而言，HTTP2 有以下有点：

- 解析速度快
- 多路复用
- 首部压缩
- 优先级更高
- 流量控制
- 服务器推送

### 3、使用服务器渲染

客户端渲染：获取 HTML 文件，根据需要下载 JavaScript 文件，运行文件，生成 DOM，在渲染。

服务器渲染：服务器返回 HTML 文件，客户端只需解析 HTML。

- 优点：首屏渲染块，SEO 好。
- 缺点：配置麻烦，增加了服务器的计算压力。

### 4、将 CSS 资源放在文件头部，JavaScript 文件放在文件底部

- CSS 执行会阻塞渲染，阻止 JS 执行
- JS 加载和执行会阻塞 HTML 解析，阻止 CSSOM 构建

如果这些 CSS、JS 标签放在 HEAD 标签里，并且需要加载和解析很久的话，那么页面就空白了。所以 JS 文件要放在底部（不阻止 DOM 解析，但会阻塞渲染），等 HTML 解析完了再加载 JS 文件，尽早向用户呈现页面的内容。
那为什么 CSS 文件还要放在头部呢？
因为先加载 HTML 再加载 CSS，会让用户第一时间看到的页面是没有样式的、“丑陋”的，为了避免这种情况发生，就要将 CSS 文件放在头部了。
另外，JS 文件也不是不可以放在头部，只要给 script 标签加上 defer 属性就可以了，异步下载，延迟执行。

### 5、善用缓存，不重复加载相同的资源

## 资源优化

### 1、静态资源使用 CDN

内容分发网络（CDN）是一组分布在多个不同地理位置的 Web 服务器。我们都知道，当服务器离用户越远时，延迟越高。CDN 就是为了解决这一问题，在多个位置部署服务器，让用户离服务器更近，从而缩短请求时间。

### 2、使用字符图标 iconfont 代替图片图标

优点：

> - 字体图标是矢量图，不会失真
> - 轻量级，加载速度快，因为字体图标都非常小
> - 灵活性，各种 CSS 效果前端控制，不需要 UI 修改
> - 兼容性，支持所有浏览器，包括 IE 低版本
> - 可维护性，建立一个项目图标之后，可一直更新迭代

缺点：

> - 与真正图片比较，效果不如图片
> - 需要 UI 学习制作图标
> - 不如图片那样容易重构

### 3、loading 图片加载

## 代码优化

### 1、 图片延迟加载

### 2、 图片懒加载

### 3、 响应式图片

响应式图片的优点是浏览器能够根据屏幕大小自动加载合适的图片。

通过 `picture` 实现

```html
<picture>
  <source srcset="banner_w1000.jpg" media="(min-width: 801px)" />
  <source srcset="banner_w800.jpg" media="(max-width: 800px)" />
  <img src="banner_w800.jpg" alt="" />
</picture>
复制代码
```

通过 `@media` 实现

```html
@media (min-width: 769px) { .bg { background-image: url(bg1080.jpg); } } @media
(max-width: 768px) { .bg { background-image: url(bg768.jpg); } }
```

### 5、 尽可能利用 CSS3 效果代替图片

有很多图片使用 CSS 效果（渐变、阴影等）就能画出来，这种情况选择 CSS3 效果更好。因为代码大小通常是图片大小的几分之一甚至几十分之一。

### 6、 if-else 对比 switch

当判断条件数量越来越多时，越倾向于使用 switch 而不是 if-else。

### 7、去除 console.log

### 8、去除 SourceMap

## 插件优化

### 1、压缩文件

在 webpack 可以使用如下插件进行压缩：

- JavaScript：UglifyPlugin
- CSS ：MiniCssExtractPlugin
- HTML：HtmlWebpackPlugin
- gzip 压缩

### 2、 Tree-shaking

## Vue 优化]

### 1、v-if 和 v-show 区分使用场景

### 2、computed 和 watch 区分使用场景

### 3、v-for 遍历必须为 item 添加 key，且避免同时使用 v-if

### 4、不需要监听的 data 属性，将它放在 data 外面

### 5、减少 ES6 转为 ES5 的冗余代码

### 6、提取公共代码
