---
title: 5个JavaScript写法小技巧分享
date: 2022-02-12 22:18:35
author: cookie
img: ../images/20.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/20.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: 5个JavaScript写法小技巧分享
categories: javascript
tags:
  - javascript
---

## 过滤空值

使用 `filter()` 过滤 “空” 值，如 `null`、`undefined` 或空字符串，可以使用 `.filter(Boolean)` 的缩写方法；

它将所有空值转为 `false` 并从列表中删除它们，优雅！

```javascript
const groceries = ["apple", null, "milk", undefined, "bread", ""];

const cleanList = groceries.filter(Boolean);

console.log(cleanList);

// 'apple', 'milk', 'bread';
```

## 数组对象解构

我们经常使用 ES6 的解构，对于一个数组，每项都是一个对象，如果想获得数组第一项的对象的某个值，可以这样写；

```javascript
const people = [
  {
    name: "Lisa",
    age: 20,
  },
  {
    name: "Pete",
    age: 22,
  },
  {
    name: "Caroline",
    age: 60,
  },
];

const [{ age }] = people;

console.log(age);

// 20
```

也可以采用逗号占位的方式指定一个项进行赋值；

```javascript
const people = [
  {
    name: "Lisa",
    age: 20,
  },
  {
    name: "Pete",
    age: 22,
  },
  {
    name: "Caroline",
    age: 60,
  },
];

const [, , caroline] = people;

console.log(caroline);

//  {
//     name: "Caroline",
//     age: 60,
//   }
```

当然，也有常见的对象解构赋值；

```javascript
const caroline = {
  firstNm: "Caroline",
  ag: 27,
};

const { firstNm: firstName, ag: age } = caroline;

console.log(firstName, age);

// Caroline, 27
```

## 分隔数字

对大数字使用分隔符号，将极大的提高可读性；这是 ES12 的新特性；

```javascript
const bigNumber = 1_000_000;
console.log(bigNumber);
// 1000000
```

## 箭头函数直接返回对象

使用箭头函数返回一个对象，为了和函数的 `{` 区分开来，在外层包一层 `(` 即可解决；

```javascript
const createPerson = (age, name, nationality) => ({
  age,
  name,
  nationality,
});

const caroline = createPerson(27, "Caroline", "US");

console.log(caroline);

// {
//   age: 27,
//   name: 'Caroline'
//   nationality: 'US',
// }
```

## await 链条

我们可以用 `filter`  和  `map` 方法接在 await 方法后形成链条过滤或映射处理获取的数据；

```javascript
const chainDirectly = (await fetch("https://www.people.com"))
  .filter((person) => age > 20)
  .filter((person) => nationality === "NL");
```
