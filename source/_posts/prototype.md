---
title: javascript 原型链
date: 2021-11-28 22:56:32
author: cookie
img: ../images/13.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/56.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: javascript 原型链
categories: javascript
tags:
  - javascript
---

# JS 中的原型和原型链

讲原型的时候，我们应该先要记住以下几个要点，这几个要点是理解**原型的关键**：

1、所有的引用类型（数组、函数、对象）可以自由扩展属性（除 null 之外）。

2、所有的引用类型都有一个`__proto__`属性(也叫**隐式原型**，它是一个普通的对象)。

3、所有的函数都有一个`prototype`属性(这也叫**显式原型**，它也是一个普通的对象)。

4、所有引用类型，它的`__ proto__`属性指向它的构造函数的`prototype`属性。

5、当试图得到一个对象的属性时，如果这个对象本身不存在这个属性，那么就会去它的`__ proto__`属性(也就是它的构造函数的`prototype`属性)中去寻找。



## 原型

我们先来看一个**原型**的例子。

```javascript
//这是一个构造函数
function Foo(name, age) {
  this.name = name;
  this.age = age;
}
/*根据要点3，所有的函数都有一个prototype属性，这个属性是一个对象
再根据要点1，所有的对象可以自由扩展属性
于是就有了以下写法*/
Foo.prototype = {
  // prototype对象里面又有其他的属性
  showName: function () {
    console.log("I'm " + this.name); //this是什么要看执行的时候谁调用了这个函数
  },
  showAge: function () {
    console.log("And I'm " + this.age); //this是什么要看执行的时候谁调用了这个函数
  },
};
var fn = new Foo("小明", 19);
/*当试图得到一个对象的属性时，如果这个对象本身不存在这个属性，那么就会去它
构造函数的'prototype'属性中去找*/
fn.showName(); //I'm 小明
fn.showAge(); //And I'm 19
```

这就是原型，很好理解。那为什么要使用原型呢？

试想如果我们要通过 Foo()来创建很多很多个对象，如果我们是这样子写的话：

```javascript
function Foo(name, age) {
  this.name = name;
  this.age = age;
  this.showName = function () {
    console.log("I'm " + this.name);
  };
  this.showAge = function () {
    console.log("And I'm " + this.age);
  };
}
```

那么我们创建出来的每一个对象，里面都有 showName 和 showAge 方法，这样就会占用很多的资源。  
而通过原型来实现的话，只需要在构造函数里面给属性赋值，而把方法写在 Foo.prototype 属性(这个属性是唯一的)里面。这样每个对象都可以使用 prototype 属性里面的 showName、showAge 方法，并且节省了不少的资源。

---

## 原型链

理解了原型，那么原型链就更好理解了。

##### 下面这段话可以帮助理解原型链

根据要点 5，当试图得到一个对象的属性时，如果这个对象本身不存在这个属性，那么就会去它构造函数的`prototype`属性中去寻找。那又因为`prototype`属性是一个对象，所以它也有一个`__proto__`属性。

那么我们来看一个例子：

```javascript
// 构造函数
function Foo(name, age) {
  this.name = name;
  this.age = age;
}
Object.prototype.toString = function () {
  //this是什么要看执行的时候谁调用了这个函数。
  console.log("I'm " + this.name + " And I'm " + this.age);
};
var fn = new Foo("小明", 19);
fn.toString(); //I'm 小明 And I'm 19
console.log(fn.toString === Foo.prototype.__proto__.toString); //true

console.log(fn.__proto__ === Foo.prototype); //true
console.log(Foo.prototype.__proto__ === Object.prototype); //true
console.log(Object.prototype.__proto__ === null); //true
```

是不是觉得有点奇怪？我们来分析一下。  
![javascript 原型链](https://image.gongweiwei.top/blog/cookie/javascript/prototype.jpg)
首先，fn 的构造函数是 Foo()。所以：  
**fn.\_\_proto\_\_=== Foo.prototype**  
又因为 Foo.prototype 是一个普通的对象，它的构造函数是 Object，所以：  
**Foo.prototype.\_\_proto\_\_=== Object.prototype**  
通过上面的代码，我们知道这个 toString()方法是在 Object.prototype 里面的，当调用这个对象的本身并不存在的方法时，它会一层一层地往上去找，一直到 null 为止。

**所以当 fn 调用 toString()时，JS 发现 fn 中没有这个方法，于是它就去 Foo.prototype 中去找，发现还是没有这个方法，然后就去 Object.prototype 中去找，找到了，就调用 Object.prototype 中的 toString()方法。**

这就是原型链，fn 能够调用 Object.prototype 中的方法正是因为存在**原型链**的机制。

另外，在使用原型的时候，一般推荐将需要扩展的方法写在**构造函数的 prototype 属性**中，避免写在`__proto__`属性里面。

**朋友们如果看懂了留个赞呗 😃，不懂可以在评论区留言。**
