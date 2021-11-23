---
title: js二维数组转化为一维数组
date: 2021-11-24 00:03:37
author: cookie
img: ../images/10.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/56.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: js二维数组转化为一维数组
categories: javascript
tags:
  - javascript
  - array
---

- 方法一
  利用 ES6
  优点：多维数组也可以，递归函数。**推荐使用，是这几种方法中最完备的**
  

```javascript
let arr2_1 = [
  [0, 1],
  [2, 3],
  [4, 5, [6]],
];

let fun2 = (arr) =>
  [].concat(...arr.map((x) => (Array.isArray(x) ? fun2(x) : x)));
let arr2_2 = fun2(arr2_1);

console.log(arr2_2); // [ 0, 1, 2, 3, 4, 5, 6 ]
```

- 方法二
  利用 ES5 的 arr.reduce(callback[, initialValue]) 实现

```javascript
let arr1_1 = [
  [0, 1],
  [2, 3],
  [4, 5, [6]],
];
let arr1_2 = arr1_1.reduce((a, b) => a.concat(b));
console.log(arr1_2); // [ 0, 1, 2, 3, 4, 5, [ 6 ] ]
```

- 方法三
  利用 apply 实现
  也是只能处理二维数组

```javascript
let arr3_1 = [
  [0, 1],
  [2, 3],
  [4, 5, [6]],
];
let arr3_2 = [].concat.apply([], arr3_1);

console.log(arr3_2); // [ 0, 1, 2, 3, 4, 5, [ 6 ] ]
```

- 方法四
  通过将数组转变为字符串，利用 str.split(',')实现。缺点是数组元素都变为字符串了
  优点是可以处理多维数组

```javascript
let arr4_1 = [
  [0, 1],
  [2, 3],
  [4, 5, [6]],
];
let arr4_2 = (arr4_1 + "").split(",").map(Number);
console.log(arr4_2); // [ 0, 1, 2, 3, 4, 5, [ 6 ] ]
```
