---
title: ES6-ES12的开发技巧
date: 2022-02-14 06:02:29
author: cookie
img: ../images/21.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/21.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: ES6-ES12的开发技巧
categories: ES6
tags:
  - javascript
  - ES6
---

## ES6

### 1、let 和 const

这两个的出现，总感觉是为了开发的代码规范而出现的。我们要逐渐放弃 var，在项目中多用 let 和 const

与 var 的区别：

- var 有变量提升，有初始化提升，值可变
- let 有变量提升，没有初始化提升，值可变
- const 有变量提升，没有初始化提升，值不可变，但如果是定义对象，则属性可变

`暂时性死区`问题说明：其实`let和const`是有变量提升的，但是没有初始化提升：

```javascript
var name = "林三心";

function fn() {
  console.log(name);
  let name = "sunshin_lin";
}
fn(); // Cannot access 'name' before initialization
```

块级作用域解决问题：

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  });
} // 5 5 5 5 5

for (let i = 0; i < 5; i++) {
  setTimeout(() => {
    console.log(i);
  });
} // 0 1 2 3 4
```

### 2、默认参数

开发中你曾遇到过这样的问题，如果参数不传进来，你就设置默认参数

```javascript
function fn(name, age) {
  var name = name || "林三心";
  var age = age || 18;
  console.log(name, age);
}
fn(); // 林三心 18
```

但是这么写确实不优雅，可以使用 ES6 的默认参数

```javascript
function fn(name = "林三心", age = 18) {
  console.log(name, age);
}
fn(); // 林三心 18
fn("sunshine", 22); // sunshine 22
```

### 3、扩展运算符

曾经的我，想要拼接多个数组，我只能这么做

```javascript
const arr1 = [1, 2, 4];
const arr2 = [4, 5, 7];
const arr3 = [7, 8, 9];

const arr = arr1.concat(arr2).concat(arr3)[(1, 2, 4, 4, 5, 7, 7, 8, 9)];
```

现在的我，可以更优雅地进行拼接

```javascript
const arr1 = [1, 2, 4];
const arr2 = [4, 5, 7];
const arr3 = [7, 8, 9];

const arr = [...arr1, ...arr2, ...arr3][(1, 2, 4, 4, 5, 7, 7, 8, 9)];
```

### 4、剩余参数

大家可能遇到过这种问题，一个函数，传入参数的个数是不确定的，这就可以用 ES6 的剩余参数

```javascript
function fn(name, ...params) {
  console.log(name);
  console.log(params);
}
fn("林三心", 1, 2); // 林三心 [ 1, 2 ]
fn("林三心", 1, 2, 3, 4, 5); // 林三心 [ 1, 2, 3, 4, 5 ]
```

### 5、模板字符串

以前的我，拼接字符串只能这么做

```javascript
const name = "林三心";
const age = "22";

console.log(name + "今年" + age + "岁啦"); // 林三心今年22岁啦
```

现在我可以这么做，会更优雅

```javascript
const name = "林三心";
const age = "22";

console.log(`${name}今年${age}岁啦`); // 林三心今年22岁啦
```

### 6、Object.keys

可以用来获取对象的 key 的集合，进而可以获得对应 key 的 value

```javascript
const obj = {
  name: "林三心",
  age: 22,
  gender: "男",
};

const keys = Object.keys(obj);
console.log(keys); // [ 'name', 'age', 'gender' ]
```

### 7、箭头函数

以前我们使用普通函数

```javascript
function fn() {}

const fn = function () {};
```

ES6 新加了`箭头函数`

```javascript
const fn = () => {};

// 如果只有一个参数，可以省略括号
const fn = (name) => {};

// 如果函数体里只有一句return
const fn = (name) => {
  return 2 * name;
};
// 可简写为
const fn = (name) => 2 * name;
// 如果返回的是对象
const fn = (name) => ({ name: name });
```

普通函数和箭头函数的区别：

- 1、箭头函数不可作为构造函数，不能使用 new
- 2、箭头函数没有自己的 this
- 3、箭头函数没有 arguments 对象
- 4、箭头函数没有原型对象

### 8、Array.prototype.forEach

ES6 新加的数组遍历方法

```javascript
const eachArr = [1, 2, 3, 4, 5]

// 三个参数：遍历项 索引 数组本身
// 配合箭头函数
eachArr.forEach((item, index, arr) => {
  console.log(item, index, arr)
})
1 0 [ 1, 2, 3, 4, 5 ]
2 1 [ 1, 2, 3, 4, 5 ]
3 2 [ 1, 2, 3, 4, 5 ]
4 3 [ 1, 2, 3, 4, 5 ]
5 4 [ 1, 2, 3, 4, 5 ]
```

### 9、Array.prototype.map

常用于返回一个处理过后的新数组

```javascript
const mapArr = [1, 2, 3, 4, 5];

// 三个参数：遍历项 索引 数组本身
// 配合箭头函数，对每一个元素进行翻倍
const mapArr2 = mapArr.map((num, index, arr) => 2 * num);
console.log(mapArr2); // [(2, 4, 6, 8, 10)];
```

### 10、Array.prototype.filter

顾名思义，用来过滤的方法

```javascript
const filterArr = [1, 2, 3, 4, 5];

// 三个参数：遍历项 索引 数组本身
// 配合箭头函数，返回大于3的集合
const filterArr2 = filterArr.filter((num, index, arr) => num > 3);
console.log(filterArr2); // [(4, 5)];
```

### 11、Array.prototype.some

some，意思就是只要有一个是真，那就返回真

```javascript
const someArr = [false, true, false, true, false];

// 三个参数：遍历项 索引 数组本身
// 配合箭头函数，只要有一个为true，就返回true，一个都true都没有，就返回false
const someArr2 = someArr.some((bol, index, arr) => bol);
console.log(someArr2); // true;
```

### 12、Array.prototype.every

every 跟 some 是相反的，some 是只要有一个就行，every 是要所有为真才返回真

```javascript
const everyArr = [false, true, false, true, false];

// 三个参数：遍历项 索引 数组本身
// 配合箭头函数，需要所有为true，才返回true，否则返回false
const everyArr2 = everyArr.every((bol, index, arr) => bol);
console.log(everyArr2); // false;
```

### 13、Array.prototype.reduce

- 第一个参数 callback 函数： pre 为上次 return 的值，next 为数组的本次遍历的项
- 第二个参数为初始值，也是第一个 pre

举两个例子：

```javascript
// 计算 1 + 2 + 3 + 4 + 5
const reduceArr = [1, 2, 3, 4, 5];
const sum = reduceArr.reduce((pre, next) => {
  return pre + next;
}, 0);
console.log(sum); // 15

// 统计元素出现个数
const nameArr = ["林三心", "sunshine_lin", "林三心", "林三心", "科比"];
const totalObj = nameArr.reduce((pre, next) => {
  if (pre[next]) {
    pre[next]++;
  } else {
    pre[next] = 1;
  }
  return pre;
}, {});
console.log(totalObj); // { '林三心': 3, sunshine_lin: 1, '科比': 1 }
```

### 14、对象属性同名简写

以前同名属性需要这么写

```javascript
const name = "林三心";
const age = "22";

const obj = {
  name: name,
  age: age,
};

console.log(obj); // { name: '林三心', age: '22' }
```

ES6 新增语法，只需这么写

```javascript
const name = "林三心";
const age = "22";

// 属性同名可简写
const obj = {
  name,
  age,
};

console.log(obj); // { name: '林三心', age: '22' }
```

### 15、Promise

`Promise`，中文名为`承诺`，承诺在哪呢？承诺在，一旦他的状态改变，就不会再改。这里就介绍基本使用，如果想要深入理解如何使用，请看我的另一篇文章[看了就会，手写 Promise 原理，最通俗易懂的版本！！！](https://juejin.cn/post/6994594642280857630 "https://juejin.cn/post/6994594642280857630")

看看基本使用

- 成功状态

```javascript
function requestData() {
  // 模拟请求
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("林三心");
    }, 1000);
  });
}

requestData().then(
  (res) => {
    console.log(res); // 一秒钟后输出 '林三心'
  },
  (err) => {
    console.log(err);
  }
);
```

- 失败状态

```javascript
function requestData() {
  // 模拟请求
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject("错误啦");
    }, 1000);
  });
}

requestData().then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.log(err); // 一秒钟后输出 '错误啦'
  }
);
```

- `all`方法
  - 接收一个 Promise 数组，数组中如有非 Promise 项，则此项当做成功
  - 如果所有 Promise 都成功，则返回成功结果数组
  - 如果有一个 Promise 失败，则返回这个失败结果

```javascript
// 如果全都为成功
function fn(time) {
  return new Promise((resolve, reject) => {
    console.log(88);
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`);
    }, time);
  });
}

Promise.all([fn(2000), fn(3000), fn(1000)]).then(
  (res) => {
    // 3秒后输出 [ '2000毫秒后我成功啦！！！', '3000毫秒后我成功啦！！！', '1000毫秒后我成功啦！！！' ]
    console.log(res);
  },
  (err) => {
    console.log(err);
  }
);

// 如果有一个失败
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve
        ? resolve(`${time}毫秒后我成功啦！！！`)
        : reject(`${time}毫秒后我失败啦！！！`);
    }, time);
  });
}

Promise.all([fn(2000, true), fn(3000), fn(1000, true)]).then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.log(err); // 3秒后输出 '3000毫秒后我失败啦！！！'
  }
);
```

- `race`方法
  - 接收一个 Promise 数组，数组中如有非 Promise 项，则此项当做成功
  - 哪个 Promise 最快得到结果，就返回那个结果，无论成功失败

```javascript
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve
        ? resolve(`${time}毫秒后我成功啦！！！`)
        : reject(`${time}毫秒后我失败啦！！！`);
    }, time);
  });
}

Promise.race([fn(2000, true), fn(3000), fn(1000)]).then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.log(err); // 1秒后输出
  }
);
```

### 16、class

以前咱们使用构造函数生成对象，这么做

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayName = function () {
  console.log(this.name);
};

const kobe = new Person("科比");
kobe.sayName(); // 科比
```

而有了 ES6 的`class`可以这么做

```javascript
class Person {
  constructor(name) {
    // 构造器
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}

const kobe = new Person("科比");
kobe.sayName(); // 科比
```

值得一提的是，`class`本质也是`function`，`class`是`function`的`语法糖`

```javascript
class Person {}

console.log(typeof Person); // function
```

除了以上，还需要知道 class 的以下知识点

静态属性和静态方法，使用`static`定义的属性和方法只能 class 自己用，实例用不了

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  static age = 22;

  static fn() {
    console.log("哈哈");
  }
}
console.log(Person.age); // 22
Person.fn(); // 哈哈

const sunshine_lin = new Person("林三心");
console.log(sunshine_lin.age); // undefined
sunshine_lin.fn(); // fn is not a function
```

`extend`继承

```javascript
class Animal {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

class Cat extends Animal {
  say() {
    console.log(this.name, this.age);
  }
}

const cat = new Cat("ketty", 5); // 继承了Animal的构造器
cat.say(); // ketty 5
```

### 17、解构赋值

以前想提取对象里的属性需要这么做

```javascript
const obj = {
  name: "林三心",
  age: 22,
  gender: "男",
};

const name = obj.name;
const age = obj.age;
const gender = obj.gender;
console.log(name, age, gender); // 林三心 22 男
```

ES6 新增了解构赋值的语法

```javascript
const obj = {
  name: "林三心",
  age: 22,
  gender: "男",
  doing: {
    morning: "摸鱼",
    afternoon: "摸鱼",
    evening: "sleep",
  },
};

const { name, age, gender } = obj;
console.log(name, age, gender); // 林三心 22 男

// 解构重名
const { name: myname } = obj;
console.log(myname); // 林三心

// 嵌套解构
const {
  doing: { evening },
} = obj;
console.log(evening); // sleep
```

也可以进行数组的解构

```javascript
const arr = [1, 2, 3];

const [a, b, c] = arr;
console.log(a, b, c); // 1 2 3

// 默认赋值
const [a, b, c, d = 5] = arr;
console.log(a, b, c, d); // 1 2 3 5

// 乱序解构
const { 1: a, 0: b, 2: c } = arr;
console.log(a, b, c); // 2 1 3
```

### 18、find 和 findIndex

- find：找到返回被找元素，找不到返回 undefined
- findIndex：找到返回被找元素索引，找不到返回-1

```javascript
const findArr = [
  { name: "科比", no: "24" },
  { name: "罗斯", no: "1" },
  { name: "利拉德", no: "0" },
];

const kobe = findArr.find(({ name }) => name === "科比");
const kobeIndex = findArr.findIndex(({ name }) => name === "科比");
console.log(kobe); // { name: '科比', no: '24' }
console.log(kobeIndex); // 0
```

### 19、for of 和 for in

- for in ：遍历方法，可遍历对象和数组
- for of ：遍历方法，只能遍历数组，不能遍历非 iterable 对象

先看 for in：

```javascript
const obj = { name: "林三心", age: 22, gender: "男" };
const arr = [1, 2, 3, 4, 5];

for (let key in obj) {
  console.log(key);
}
// name
// age
// gender

for (let index in arr) {
  console.log(index);
}
// 0 1 2 3 4
```

再看 for of：

```javascript
for (let item of arr) {
  console.log(item);
}
// 1 2 3 4 5
```

### 20、Set 和 Map

- Set

先说说`Set`的基本用法

```javascript
// 可不传数组
const set1 = new Set();
set1.add(1);
set1.add(2);
console.log(set1); // Set(2) { 1, 2 }

// 也可传数组
const set2 = new Set([1, 2, 3]);
// 增加元素 使用 add
set2.add(4);
set2.add("林三心");
console.log(set2); // Set(5) { 1, 2, 3, 4, '林三心' }
// 是否含有某个元素 使用 has
console.log(set2.has(2)); // true
// 查看长度 使用 size
console.log(set2.size); // 5
// 删除元素 使用 delete
set2.delete(2);
console.log(set2); // Set(4) { 1, 3, 4, '林三心' }
```

再说说`Set`的不重复性

```javascript
// 增加一个已有元素，则增加无效，会被自动去重
const set1 = new Set([1]);
set1.add(1);
console.log(set1); // Set(1) { 1 }

// 传入的数组中有重复项，会自动去重
const set2 = new Set([1, 2, "林三心", 3, 3, "林三心"]);
console.log(set2); // Set(4) { 1, 2, '林三心', 3 }
```

`Set`的不重复性中，要注意`引用数据类型和NaN`

```javascript
// 两个对象都是不同的指针，所以没法去重
const set1 = new Set([1, { name: "林三心" }, 2, { name: "林三心" }]);
console.log(set1); // Set(4) { 1, { name: '林三心' }, 2, { name: '林三心' } }

// 如果是两个对象是同一指针，则能去重
const obj = { name: "林三心" };
const set2 = new Set([1, obj, 2, obj]);
console.log(set2); // Set(3) { 1, { name: '林三心' }, 2 }

// 咱们都知道 NaN !== NaN，NaN是自身不等于自身的，但是在Set中他还是会被去重
const set = new Set([1, NaN, 1, NaN]);
console.log(set); // Set(2) { 1, NaN }
```

利用 Set 的不重复性，可以实现数组去重

```javascript
const arr = [1, 2, 3, 4, 4, 5, 5, 66, 9, 1];

// Set可利用扩展运算符转为数组哦
const quchongArr = [...new Set(arr)];
console.log(quchongArr); // [1,  2, 3, 4, 5, 66, 9]
```

- Map

`Map`对比`object`最大的好处就是，key 不受`类型限制`

```javascript
// 定义map
const map1 = new Map();
// 新增键值对 使用 set(key, value)
map1.set(true, 1);
map1.set(1, 2);
map1.set("哈哈", "嘻嘻嘻");
console.log(map1); // Map(3) { true => 1, 1 => 2, '哈哈' => '嘻嘻嘻' }
// 判断map是否含有某个key 使用 has(key)
console.log(map1.has("哈哈")); // true
// 获取map中某个key对应的value 使用 get(key)
console.log(map1.get(true)); // 2
// 删除map中某个键值对 使用 delete(key)
map1.delete("哈哈");
console.log(map1); // Map(2) { true => 1, 1 => 2 }

// 定义map，也可传入键值对数组集合
const map2 = new Map([
  [true, 1],
  [1, 2],
  ["哈哈", "嘻嘻嘻"],
]);
console.log(map2); // Map(3) { true => 1, 1 => 2, '哈哈' => '嘻嘻嘻' }
```

## ES7

### 21、includes

传入元素，如果数组中能找到此元素，则返回 true，否则返回 false

```javascript
const includeArr = [1, 2, 3, "林三心", "科比"];

const isKobe = includeArr.includes("科比");
console.log(isKobe); // true
```

跟 indexOf 很像，但还是有区别的

```javascript
const arr = [1, 2, NaN];

console.log(arr.indexOf(NaN)); // -1  indexOf找不到NaN
console.log(arr.includes(NaN)); // true includes能找到NaN
```

### 22、求幂运算符

以前求幂，我们需要这么写

```javascript
const num = Math.pow(3, 2); // 9
```

ES7 提供了求幂运算符：`**`

```javascript
const num = 3 ** 2; // 9
```

## ES8

### 23、Object.values

可以用来获取对象的 value 的集合

```javascript
const obj = {
  name: "林三心",
  age: 22,
  gender: "男",
};

const values = Object.values(obj);
console.log(values); // [ '林三心', 22, '男' ]
```

### 24、Object.entries

可以用来获取对象的键值对集合

```javascript
const obj = {
  name: "林三心",
  age: 22,
  gender: "男",
};

const entries = Object.entries(obj);
console.log(entries);
// [ [ 'name', '林三心' ], [ 'age', 22 ], [ 'gender', '男' ] ]
```

### 25、async/await

这个是很常用的语法了，我的理解就是：**以同步方式执行异步操作**

我们平时可能会遇到这种场景，接口一，请求到数据一，而数据一被当做请求二的参数去请求数据二，我们会用 Promise 这么做

```javascript
function fn() {
  // 模拟第一次请求
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(5);
    }, 1000);
  }).then((res) => {
    // 模拟第二次请求
    new Promise((resolve, reject) => {
      setTimeout(() => {
        // 拿第一次请求的数据去乘10，当做第二次请求的数据
        resolve(res * 10);
      }, 2000);
    }).then((sres) => {
      console.log(sres);
    });
  });
}
fn(); // 1 + 2 = 3 3秒后输出 50
```

这样的嵌套是不美观的，如果有很多个接口，那就会嵌套很多层，此时我们可以使用 async/await 来以同步方式执行异步，注意以下几点：

- await 只能在 async 函数里使用
- await 后面最好接 Promise，如果后面接的是普通函数则会直接执行
- async 函数返回的是一个 Promise

```javascript
function fn1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(5);
    }, 1000);
  });
}

function fn2(data) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(data * 10);
    }, 2000);
  });
}

async function req() {
  // 同步方式执行异步，像排队一样
  const data1 = await fn1(); // 等待1秒后返回数据再往下执行
  const data2 = await fn2(data1); // 拿data1去请求2秒后，往下走
  console.log(data2); // 总共3秒后 输出 50
}
req();
```

## ES9

### 26、for await of

我们来看以下场景哈

```javascript
function fn(time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`);
    }, time);
  });
}

fn(3000).then((res) => console.log(res));
fn(1000).then((res) => console.log(res));
fn(2000).then((res) => console.log(res));

// 结果是

// 1000毫秒后我成功啦！！！
// 2000毫秒后我成功啦！！！
// 3000毫秒后我成功啦！！！
```

但是我想要这个结果

```javascript
// 3000毫秒后我成功啦！！！
// 1000毫秒后我成功啦！！！
// 2000毫秒后我成功啦！！！
```

第一时间我们肯定想到的是`async/await`

```javascript
function fn(time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`);
    }, time);
  });
}

async function asyncFn() {
  // 排队
  const data1 = await fn(3000);
  console.log(data1); // 3秒后 3000毫秒后我成功啦！！！
  const data2 = await fn(1000);
  console.log(data2); // 再过1秒 1000毫秒后我成功啦！！！
  const data3 = await fn(2000);
  console.log(data3); // 再过2秒 2000毫秒后我成功啦！！！
}
```

但是上面代码也是有缺点的，如果有几十个，那不是得写几十个 await，有没有一种方法可以通过循环来输出呢？

```javascript
function fn(time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${time}毫秒后我成功啦！！！`);
    }, time);
  });
}

async function asyncFn() {
  const arr = [fn(3000), fn(1000), fn(1000), fn(2000), fn(500)];
  for await (let x of arr) {
    console.log(x);
  }
}

asyncFn();
// 3000毫秒后我成功啦！！！
// 1000毫秒后我成功啦！！！
// 1000毫秒后我成功啦！！！
// 2000毫秒后我成功啦！！！
// 500毫秒后我成功啦！！！
```

### 27、Promise.finally

新增的 Promise 方法，无论失败或者成功状态，都会执行这个函数

```javascript
// cheng
new Promise((resolve, reject) => {
  resolve("成功喽");
})
  .then(
    (res) => {
      console.log(res);
    },
    (err) => {
      console.log(err);
    }
  )
  .finally(() => {
    console.log("我是finally");
  });

new Promise((resolve, reject) => {
  reject("失败喽");
})
  .then(
    (res) => {
      console.log(res);
    },
    (err) => {
      console.log(err);
    }
  )
  .finally(() => {
    console.log("我是finally");
  });
```

## ES10

### 28、Array.flat

有一个二维数组，我想让他变成一维数组：

```javascript
const arr = [1, 2, 3, [4, 5, 6]];

console.log(arr.flat()); // [ 1, 2, 3, 4, 5, 6 ]
```

还可以传参数，参数为降维的次数

```javascript
const arr = [1, 2, 3, [4, 5, 6, [7, 8, 9]]];

console.log(arr.flat(2)); // [(1, 2, 3, 4, 5, 6, 7, 8, 9)];
```

如果传的是一个无限大的数字，那么就实现了多维数组(无论几维)降为一维数组

```javascript
const arr = [1, 2, 3, [4, 5, 6, [7, 8, 9, [10, 11, 12]]]];

console.log(arr.flat(Infinity)); // [(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12)];
```

### 29、Array.flatMap

现在给你一个需求

```javascript
let arr = ["科比 詹姆斯 安东尼", "利拉德 罗斯 麦科勒姆"];
```

将上面数组转为

```javascript
["科比", "詹姆斯", "安东尼", "利拉德", "罗斯", "麦科勒姆"];
```

第一时间想到`map + flat`

```javascript
console.log(arr.map((x) => x.split(" ")).flat());
// [ '科比', '詹姆斯', '安东尼', '利拉德', '罗斯', '麦科勒姆' ]
```

`flatMap`就是`flat + map`，一个方法顶两个

```javascript
console.log(arr.flatMap((x) => x.split(" ")));
// [ '科比', '詹姆斯', '安东尼', '利拉德', '罗斯', '麦科勒姆' ]
```

### 30、BigInt

`BigInt`是 ES10 新加的一种 JavaScript 数据类型，用来表示表示大于  `2^53 - 1`  的整数，`2^53 - 1`是 ES10 之前，JavaScript 所能表示最大的数字

```javascript
const theBiggestInt = 9007199254740991n;

const alsoHuge = BigInt(9007199254740991);
// 9007199254740991n

const hugeString = BigInt("9007199254740991");
// 9007199254740991n

const hugeHex = BigInt("0x1fffffffffffff");
// 9007199254740991n

const hugeBin = BigInt(
  "0b11111111111111111111111111111111111111111111111111111"
);
// 9007199254740991n
```

哦对了，既然是 JavaScript 新的数据类型，那他的`typeof`是啥？

```javascript
const bigNum = BigInt(1728371927189372189739217);
console.log(typeof bigNum); // bigint
```

所以以后面试官问你 JavaScript 有多少种数据类型，别傻傻答 6 种了，要答 8 种，把 ES6 的`Symbol`和 ES10 的`BigInt`也加上去

### 31、Object.fromEntries

前面 ES8 的`Object.entries`是把`对象转成键值对数组`，而`Object.fromEntries`则相反，是把`键值对数组转为对象`

```javascript
const arr = [
  ["name", "林三心"],
  ["age", 22],
  ["gender", "男"],
];

console.log(Object.fromEntries(arr)); // { name: '林三心', age: 22, gender: '男' }
```

他还有一个用处，就是把`Map转为对象`

```javascript
const map = new Map();
map.set("name", "林三心");
map.set("age", 22);
map.set("gender", "男");

console.log(map); // Map(3) { 'name' => '林三心', 'age' => 22, 'gender' => '男' }

const obj = Object.fromEntries(map);
console.log(obj); // { name: '林三心', age: 22, gender: '男' }
```

### 32、String.trimStart && String.trimEnd

咱们都知道 JavaScript 有个 trim 方法，可以清除字符串首尾的空格

```javascript
const str = "    林三心    ";
console.log(str.trim()); // '林三心'
```

trimStart 和 trimEnd 用来单独去除字符串的首和尾的空格

```javascript
const str = "    林三心    ";

// 去除首部空格
console.log(str.trimStart()); // '林三心   '
// 去除尾部空格
console.log(str.trimEnd()); // '   林三心'
```

## ES11

### 33、Promise.allSettled

ES11 新增的 Promise 的方法

- 接收一个 Promise 数组，数组中如有非 Promise 项，则此项当做成功
- 把每一个 Promise 的结果，集合成数组，返回

```javascript
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve
        ? resolve(`${time}毫秒后我成功啦！！！`)
        : reject(`${time}毫秒后我失败啦！！！`);
    }, time);
  });
}

Promise.allSettled([fn(2000, true), fn(3000), fn(1000)]).then((res) => {
  console.log(res);

  // 3秒后输出
  /* [
        ({ status: "fulfilled", value: "2000毫秒后我成功啦！！！" },
        { status: "rejected", reason: "3000毫秒后我失败啦！！！" },
        { status: "rejected", reason: "1000毫秒后我失败啦！！！" })
    ]; */
});
```

### 34、?. 和 ??

- 先说说`?.`，中文名为`可选链`

比如我们需要一个变量，是数组且有长度，才做某些操作

```javascript
const list = null;
// do something
if (list && list.length) {
  // do something
}

// 使用可选链
const list = null;
// do something
if (list?.length) {
  // do something
}
```

比如有一个对象，我要取一个可能不存在的值，甚至我们都不确定 obj 是否存在

```javascript
const obj = {
  cat: {
    name: "哈哈",
  },
};
const dog = obj && obj.dog && obj.dog.name; // undefined

// 可选链
const obj = {
  cat: {
    name: "哈哈",
  },
};
const dog = obj?.dog?.name; // undefined
```

比如有一个数组，我不确定它存不存在，存在的话就取索引为 1 的值

```javascript
const arr = null;
// do something
const item = arr && arr[1];

// 可选链
const arr = null;
// do something
const item = arr?.[1];
```

比如有一个函数，我们不确定它存不存在，存在的话就执行它

```javascript
const fn = null;
// do something
const res = fn && fn();

// 可选链
const fn = null;
// do something
const res = fn?.();
```

- 再说说`??`，中文名为`空位合并运算符`

请看以下代码，咱们使用`||`运算符，只要左边是`假值`，就会返回右边的数据

```javascript
const a = 0 || "林三心"; // 林三心
const b = "" || "林三心"; // 林三心
const c = false || "林三心"; // 林三心
const d = undefined || "林三心"; // 林三心
const e = null || "林三心"; // 林三心
```

而`??`和`||`最大的区别是，在`??`这，只有`undefined和null`才算假值

```javascript
const a = 0 ?? "林三心"; // 0
const b = "" ?? "林三心"; // ''
const c = false ?? "林三心"; // false
const d = undefined ?? "林三心"; // 林三心
const e = null ?? "林三心"; // 林三心
```

## ES12

### 35、Promise.any

E12 新增的 Promise 的方法

- 接收一个 Promise 数组，数组中如有非 Promise 项，则此项当做成功
- 如果有一个 Promise 成功，则返回这个成功结果
- 如果所有 Promise 都失败，则报错

```javascript
// 当有成功的时候，返回最快那个成功
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve
        ? resolve(`${time}毫秒后我成功啦！！！`)
        : reject(`${time}毫秒后我失败啦！！！`);
    }, time);
  });
}

Promise.any([fn(2000, true), fn(3000), fn(1000, true)]).then(
  (res) => {
    console.log(res); // 1秒后 输出  1000毫秒后我成功啦
  },
  (err) => {
    console.log(err);
  }
);

// 当全都失败时
function fn(time, isResolve) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      isResolve
        ? resolve(`${time}毫秒后我成功啦！！！`)
        : reject(`${time}毫秒后我失败啦！！！`);
    }, time);
  });
}

Promise.any([fn(2000), fn(3000), fn(1000)]).then(
  (res) => {
    console.log(res);
  },
  (err) => {
    console.log(err); // 3秒后 报错 all Error
  }
);
```

### 36、数字分隔符

数字分隔符可以让你在定义长数字时，更加地一目了然

```javascript
const num = 1000000000;

// 使用数字分隔符
const num = 1_000_000_000;
```

### 37、||= 和 &&=

```javascript
或等于(||=)   a ||= b 等同于 a || (a = b);

且等于(&&=)   a &&= b 等同于 a && (a = b);

```

## 不知道是 ES 几

### 38、对象计算属性

我们经常碰到这样的问题，无论是在微信小程序还是 React 中，我们需要根据某个条件去修改某个数据

```javascript
if (type === "boy") {
  this.setData({
    boyName: name,
  });
} else if (type === "girl") {
  this.setData({
    girlName: name,
  });
}
```

我也不知道这个新特性叫啥，我就自己取名叫`属性动态属性`哈哈哈

```javascript
this.setData({
  [`${type}Name`]: name,
});
```

## 补充

### 39、Symbol

#### 应用场景 1：使用 Symbol 来作为对象属性名

平常我们对象的属性都是字符串

```javascript
const obj = {
  name: "Sunshine_Lin",
  age: 23,
};
console.log(obj["name"]); // 'Sunshine_Lin'
console.log(obj["age"]); // 23
```

其实也可以用 Symbol 来当做属性名

```javascript
const gender = Symbol("gender");
const obj = {
  name: "Sunshine_Lin",
  age: 23,
  [gender]: "男",
};
console.log(obj["name"]); // 'Sunshine_Lin'
console.log(obj["age"]); // 23
console.log(obj[gender]); // 男
```

但是 Symbol 作为属性的属性不会被枚举出来，这也是`JSON.stringfy(obj)`时，Symbol 属性会被排除在外的原因

```javascript
console.log(Object.keys(obj)); // [ 'name', 'age' ]
for (const key in obj) {
  console.log(key); // name age
}
console.log(JSON.stringify(obj)); // {"name":"Sunshine_Lin","age":23}
```

其实想获取 Symbol 属性也不是没办法。

```javascript
// 方法一
console.log(Object.getOwnPropertySymbols(obj)); // [ Symbol(gender) ]
// 方法二
console.log(Reflect.ownKeys(obj)); // [ 'name', 'age', Symbol(gender) ]
```

#### 应用场景 2：使用 Symbol 来替代常量

有以下场景

```javascript
// 赋值
const one = "oneXin";
const two = "twoXin";

function fun(key) {
  switch (key) {
    case one:
      return "one";
      break;
    case two:
      return "two";
      break;
  }
}
```

如果变量少的话还好，但是变量多的时候，赋值命名很烦，可以利用 Symbol 的唯一性

```javascript
const one = Symbol();
const two = Symbol();
```

#### 应用场景 3：使用 Symbol 定义类的私有属性

以下例子，PASSWORD 属性无法在实例里获取到

```javascript
class Login {
  constructor(username, password) {
    const PASSWORD = Symbol();
    this.username = username;
    this[PASSWORD] = password;
  }
  checkPassword(pwd) {
    return this[PASSWORD] === pwd;
  }
}

const login = new Login("123456", "hahah");

console.log(login.PASSWORD); // 报错
console.log(login[PASSWORD]); // 报错
console.log(login[PASSWORD]); // 报错
```
