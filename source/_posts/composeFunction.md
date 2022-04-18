---
title: compose 组合式函数
date: 2022-04-18 23:47:18 
author: cookie
img: ../images/25.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/25.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: javascript 
categories: javascript
tags:
  - javascript
  - function
---

# compose 组合式函数

## 概念

- 将需要嵌套执行的函数平铺
- 嵌套执行指的是，一个函数的返回值将作为另一个函数的参数
- 实质是在函数式编程中，将几个具有特点的函数拼凑在一起，让他们结合，形成一个组合式函数

## 作用

- 实现函数式编程中的 Ponintfree，是我们专注于转换而不是数据

## 特性

- 都有共同的参数
- 执行顺序是从右到左
- 前面函数的执行结果交给后面函数处理

## 实现

### 简单实现

```javascript
//最简单的实现方式
let calculate = (x) => (x *= x + 10);
console.log(calculate(10)); // 200

// 函数实现
let add = (x) => x + 10;
let multiply = (y) => y * 10;
console.log(multiply(add(10))); // 200
```

### 闭包实现

```javascript
let add = (x) => x + 10;

let multiply = (y) => y * 10;

let compose = (f, g) => {
  return function (x) {
    return f(g(x));
  };
};
let calculate = compose(multiply, add);
console.log(calculate(10));
```

### 通用型 compose 组合函数

```javascript
let compose = function () {
  let args = [].slice().call(arguments);
  return function (x) {
    return args.reduceRight((result, callback) => {
      return callback(result);
    }, x);
  };
};

let calculate = compose(multiply, add, add);
console.log(calculate(10));
```

### 终极版 -- ES6 语法实现

```javascript
const compose =
  (...args) =>
  (x) =>
    args.reduceRight((res, cb) => cb(res), x);
```

