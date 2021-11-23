---
title: 元素水平垂直居中
date: 2021-11-16 21:28:10
author: cookie
img: ../images/03.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/34.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: 元素水平垂直居中
categories: CSS
tags:
  - CSS
  - 居中
---
#### 元素垂直居中的几种方法

##### 1、行内元素居中

```HTML
<div class="box">
  <span>hello</span>
</div>
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;

  text-align: center; /* 规定元素中的文本的水平对齐方式 */
}
.box span {
  line-height: 200px;
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;

  
  text-align: center;
  display: table-cell;
  vertical-align: middle;
}
```

##### 2、块元素居中

```HTML
<div class="box">
  <div></div>
</div>
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;
  display: flex;
  align-items: center;
  justify-content: center;
}
.box div {
  width: 100px;
  height: 50px;
  background-color: #fff;
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;

  position: relative;
}
.box div {
  background-color: green;
  position: absolute;
  width: 50px;
  height: 100px;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;
  /* 规定元素中的文本的水平对齐方式 */
  position: relative;
}
.box div {
  width: 50px;
  height: 100px;
  background-color: green;
  left: 50%;
  right: 50%;
  transform: translate(-50%, -50%);
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;
  /* 规定元素中的文本的水平对齐方式 */
  display: flex;
}
.box div {
  width: 100px;
  height: 50px;
  background-color: green;
  margin: auto;
}
```

```CSS
.box {
  width: 200px;
  height: 200px;
  background-color: red;

  display: -webkit-box;
  -webkit-box-pack: center;
  -webkit-box-align: center;
  -webkit-box-orient: vertical;
}
.box div {
  width: 50px;
  height: 100px;
  background-color: green;
}
```