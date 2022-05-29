---
title: compose 函数
date: 2022-05-29 23:50:05
author: cookie
img: ../images/27.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/27.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: compose 函数手写原理
categories: compose
tags:
  - compose
---

#### compose 代码手写

###### compose 函数可以接收多个独立的函数作为参数，然后将这些函数进行组合串联，最后返回一个“组合函数”。

##### ES5

```javascript
const compose = function () {
  // 将接收的参数存到一个数组， args == [multiply, add]
  const args = [].slice.apply(arguments);
  return function (x) {
    return args.reduceRight((res, cb) => cb(res), x);
  };
};

// 我们来验证下这个方法
let calculate = compose(multiply, add);
let res = calculate(10);
console.log(res); // 结果还是200
```

##### ES6

```javascript
const compose =
  (...args) =>
  (x) =>
    args.reduceRight((res, cb) => cb(res), x);
```

#### pipe 函数手写

###### pipe 函数跟 compose 函数的作用是一样的，也是将参数铺平。只不过他的顺序是从左往右。

##### ES5 手写

```javascript
const pipe = function () {
  const args = [].slice.apply(arguments);
  return function (x) {
    return args.reduce((res, cb) => cb(res), x);
  };
};

// 参数顺序改为从左往右
let calculate = pipe(add, multiply);
let res = calculate(10);
console.log(res); // 结果还是200
```

### ES6 手写

```javascript
const pipe =
  (...args) =>
  (x) =>
    args.reduce((res, cb) => cb(res), x);
```
