---
title: vue 侦听器 watch
date: 2022-02-24 22:21:56
author: cookie
img: ../images/23.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/23.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: vue 侦听器 watch
categories: vue
tags:
  - vue
---

### vue 侦听器 watch

在 vue 中， 使用侦听器 watch 来响应数据的变化。watch 的用法大概有三种。下面的代码块中显示的是 watch 的一种简单实现。

```javascript
export default {
  data:{
    return {
      name: "cookie"
    }
  },
  watch:{
    name(newVal, oldVal){
      // ...
    }
  }
}
```

直接写一个侦听器函数，当每次监听到变量发生改变时，执行函数。也可以在所处的侦听器数据后面直接加一条字符串形式的方法名。

```javascript
export default {
  watch: {
    name: "changeFun",
  },
};
```

#### immediate 和 handler

简单的侦听用法不能侦听到侦听的变量第一次被赋值时的改变。所以，当我们想要 在最初绑定值的时候也要执行函数，则就需要用到 immediate 属性。

```javascript
export default {
  watch: {
    name: {
      handler(newVal, oldVal) {},
      immediate: true,
    },
  },
};
```

监听的数据后面写成对象形式，包含 handler 和 immediate，之前我们写的函数其实就是在写这个 handler 方法。

immediate 表示在 watch 中首次绑定的时候，是否执行 handler，值为 true 则表示在 watch 中声明的时候，就立即执行 handler 函数，值为 false， 则和一般使用 watch 一样，在数据发生变化的时候才会触发 handler 函数。

#### deep

当需要监听一个对象的改变时，普通的 watch 方法无法监听到对象内部属性的改变，只有 data 中的属性才能监听到变化，此时就需要 deep 属性对对象进行深度监听。

```javascript
export default {
  watch: {
    obj: {
      handler (newVal, oldVal){
        // ...
      },
      deep: true,
      immediate: true
    }
  }
}
```

设置 `deep: true` 则可以监听到 obj 的变化，此时会给 obj 的所有属性都加上这个监听器，当对象属性较多时，每个属性的变化都会执行 handler。如果只需要监听对象中的一个属性值，则可以做以下优化，使用字符串的形式监听对象属性：

```javascript
export default {
  watch: {
    "obj.a": {
      handler(newVal, oldVal) {
        // ...
      },
      deep: true,
      immediate: true,
    },
  },
};
```

这样，只会给对象的某个属性添加侦听器。

数组的变化不需要通过深度监听，对象数组中的对象属性的变化则需要 deep 深度监听。

##### 最后，watch 可以侦听数组的变化，但是数组中某个值改变是监听不了的，这是 watch 故意这样做的。因为数组可能是一组非常庞大的数据，如果满足数组值的变化监听，会非常消耗性能，vue 故意没有做。但是可以监听到数组长度的变化（包括多维数组）
