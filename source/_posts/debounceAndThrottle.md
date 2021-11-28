---
title: vue 防抖节流
date: 2021-11-26 00:26:28
author: cookie
img: ../images/04.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/34.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: 防抖节流
categories: vue
tags:
  - vue
  - function
---

# Vue 最新防抖方案

**函数防抖（debounce）**：当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，如果设定的时间到来之前，又一次触发了事件，就重新开始延时。举个栗子，持续触发 scroll 事件时，并不执行 handle 函数，当 1000 毫秒内没有触发 scroll 事件时，才会延时触发 scroll 事件。

**函数节流（throttle）**：当持续触发事件时，保证一定时间段内只调用一次事件处理函数。节流通俗解释就比如我们水龙头放水，阀门一打开，水哗哗的往下流，秉着勤俭节约的优良传统美德，我们要把水龙头关小点，最好是如我们心意按照一定规律在某个时间间隔内一滴一滴的往下滴。举个栗子，持续触发 scroll 事件时，并不立即执行 handle 函数，每隔 1000 毫秒才会执行一次 handle 函数。

**防抖实例：**

```javascript
<script>
    const delay = (function () {
        let timer = 0
        return function (callback, ms) {
            clearTimeout(timer)
            timer = setTimeout(callback, ms)
        }
    })()
    export default {
        methods：{
            fn() {
                delay(() => {
                    //执行部分
                }, 500)
            }
        }
    }
</script>
```

**节流实例：**

```javascript
var throttle = function (func, delay) {
    var timer = null;
    return function () {
        var context = this;
        var args = arguments;
        if (!timer) {
            timer = setTimeout(function () {
                func.apply(context, args);
                timer = null;
            }, delay);
        }
    };
};
function handle() {
    console.log(Math.random());
}
window.addEventListener("scroll", throttle(handle, 1000));
```
