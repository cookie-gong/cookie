---
title: vue-router
date: 2021-11-16 21:32:19
author: cookie
img: ../images/09.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/34.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: vue-router
categories: vue-router
tags:
  - vue
  - router
  - vue-router
---
# vue-router

## vue-router 基础知识梳理

使用`Vue.js`，我们已经可以通过组合组件来组成应用程序，当你要把`vue-router`添加进来，我们需要做的是，将组件(`components`)映射到路由(`routes`)，然后告诉 `Vue Router` 在哪里渲染它们。

### vue-router 初步使用

```html
<div>
  <!-- 使用 router-link 组件来导航 -->
  <!-- 通过传入 to 属性指定链接 -->
  <!-- <router-link> 默认会渲染成一个带动态样式的 a 标签 -->
  <router-link to="/foo">Go to Foo</router-link>
  <router-link to="/bar">Go to Bar</router-link>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>
```

```javascript
import Vue from 'vue'
import VueRouter from 'vue-router'
Vue.use(VueRouter)
const routes = [
  {path: '/foo', component: Foo},
  {path: '/bar', component: Bar},
]
const router = new VueRouter({
  routes
})

const app = new Vue({
  router
}).$mount("#app")
```

通过注入路由器，我们可以在任何组件内通过 `this.\$router` 访问路由器，也可以通过 `this.$route` 访问当前路由。

使用 `this.$router` 的原因是我们并不想在每个独立需要封装路由的组件中都导入路由。

### 动态路由匹配

```javascript
routes: [
  {path: '/user/:id', component: User}
]
```

当一个“路径参数”使用冒号标记。当匹配到一个路由时，参数值会被设置到 `this.$route.params`，可以在每个组件内使用。于是，我们可以更新User模板，输出当前用户的 ID ：

```HTML
<div>{{$route.params.id}}</div>
```

#### 响应路由参数的变化

提醒一下，当使用路由参数时，例如从 `/user/foo` 导航到 `/user/bar` ，原来的组件实例会被复用。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。不过，这也意味着组件的生命周期钩子不会再被调用。  
复用组件时，想对路由参数的变化做出响应的话，你可以简单地 `watch`（监测变化） `$route` 对象：

```javascript
watch: {
  $route(to, from){
    // 对路由变化作出响应...
  }
}
```

或者使用2.2中引入的 `beforeRouteUpdate` 导航守卫：

```javascript
beforeRouteUpdate(to, from, next){
  // react to route changes...
  // don't forget to call next()
}
```

#### 匹配优先级

有时候，同一个路径可以匹配多个路由，此时，匹配的优先级就按照路由的定义顺序：路由定义得越早，优先级越高。

### 嵌套路由

```HTML
<div id="app">
  <router-view></router-view>
</div>
```

```javascript
const router = new VueRouter({
  routes: [{path: '/user/:id', component: User}]
})
```

这里的 `<router-view>` 是最顶层的出口，渲染最高级路由匹配到的组件。同样地，一个被渲染组件同样可以包含自己的嵌套 `<router-view>` 。例如，在 User 组件的模板添加一个 `<router-view>`:

```HTML
<div id="home">
  <router-view></router-view>
</div>
```

要在嵌套的出口中渲染组件，需要在 `VueRouter` 的参数中使用 `children` 配置：

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/user/:id',
      name: 'user',
      component: User,
      children: [
        /* 提供一个空的子路由 */
        {
          path: '',
          component: UserHome
        },
        {
          path: 'profile',
          name: 'profile',
          component: UserProfile
        },
        {
          path: 'posts',
          name: 'posts',
          component: UserPosts
        },
      ]
    }
  ]
})
```

**注意：以 / 开头的嵌套路径会被当做根路径,这让你充分的使用嵌套组件而无须设置嵌套的路径**

### 编程式导航

除了使用 `<router-link>` 创建 a 标签来定义导航链接，我们还可以借助 `router` 的实例方法，通过编写代码来实现。

**注意：在 Vue 实例内部，你可以通过 `$router` 访问路由实例。因此你可以调用 `this.$router.push`**

想要导航到不同的URL，则使用 `router.push` 方法。这个方法会向 `history` 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的URL。  
当你点击 `<router-link>` 时，这个方法会在内部调用，所以说，点击`<router-link :to="...">` 等同于调用 `this.$router.push(...)`

声明式

编程式

`<router-link :to="...">`

`router.push(...)`

该方法的参数可以是一个字符串路径，或者一个描述地址的对象。例如：

```javascript
// 字符串
router.push('home')

// 对象
router.push({path: 'home'})

// 命名的路由
router.push({name: 'user', params: {userId: '123'}})

// 带查询参数，变成 /register?plan=private
router.push({path: 'register', query: {plan: 'private'}})
```

**注意：如果提供了 `path`，`params` 会被忽略，你需要提供路由的 `name` 或手写完整的带有参数的 `path`**

```javascript
const userId = '123'

// -> /user/123
router.push({name: 'user', params: {userId}})

// -> /user/123
router.push(path: `/user/${userId}`)

// 这里的 params 不生效
// -> /user
router.push({path: '/user', params: {userId}})
```

**注意：如果目的地和当前路径相同，只有参数发生了变化（比如一个用户资料到另一个 `/user/1` -> `/user/2`），你需要使用 `beforeRouteUpdate` 来响应这个变化**

#### router.replace()

`router.replace` 和 `router.push` 很像，唯一的不用就是，它不会向 `history` 添加新纪录，而是跟它的方法名一样 —— 替换掉当前的 `history` 记录。

声明式

编程式

`<router-link :to="..." replace>`

`router.replace(...)`

#### router.go(n)

这个方法的参数是一个整数，意思是在 `history` 记录中向前或者后退多少步，类似 `window.history.go(n)`

```javascript
// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)

// 后退一步记录，等同于 history.back()
router.go(-1)

// 前进3步记录
router.go(3)

// 如果 history 记录不够用，失败
router.go(-100)
router.go(100)
```

#### 操作 History

你也许注意到 `router.push`、`router.replace` 和 `router.go` 跟 `window.history.pushState`、 `window.history.replaceState` 和 `window.history.go` 好像，实际上它们确实是效仿 `window.history` API 的。  
还有值得提及的， Vue Router 的导航方法(`push`、`replace`、`go`)在各类路由模式(`history`、 `hash` 和 `abstract`)下表现一致。

### 路由命名

有时候，通过一个名称来标识一个路由显得更方便一些，特别是在链接一个路由，或者是执行一些跳转的时候。你可以在创建 `Router` 实例的时候，在 `routes` 配置中给某个路由设置名称。

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/home/:userId',
      name: 'home',
      component: User
    }
  ]
})
```

要链接到一个命名路由，可以给 `router-link` 的 `to` 属性传一个对象：

```HTML
<router-link :to="{name: 'home', params: {userId: 123}}">Home</router-link>
```

这跟代码调用 `router.push()` 是一回事：

```javascript
router.push({name: 'home', params: {userId: 123}})
```

这两种方式都会把路由导航到 `/home/123` 路径。

### 重定向和别名

#### 重定向

重定向也是通过 `routes` 配置来完成，下面例子是从 `/a` 重定向到 `/b`：

```javascript
const router = new VueRouter({
  routes: [
    {path: '/a', redirect: '/b'}
  ]
})
```

重定向的目标也可以是一个命名的路由：

```javascript
const router = new VueRouter({
  routes: [
    {path: '/a', redirect: {name: 'foo'}}
  ]
})
```

甚至是一个方法，动态返回重定向目标：

```javascript
const router = new VueRouter({
  routes: [
    {path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})
```

#### 别名

“重定向”的意思是，当用户访问 `/a` 时，URL 将会被替换成 `/b`， 然后匹配路由为 `/b`，那么“别名”又是什么呢？

**`/a` 的别名是 `/b`，意味着，当用户访问 ‘/b’ 时，URL 会保持为 `/b`，但是路由匹配则为 `/a`，就像用户访问 `/a` 一样。**

上面对应的路由配置为：

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/a',
      component: A,
      alias: '/b'
    }
  ]
})
```

“别名”的功能让你可以自由地将 UI 结构映射到任意的 URL，而不是受限于配置地嵌套路由结构。

### 路由组件传参

在组件中使用 `$route` 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。

以解耦的方式使用 props 进行参数传递，主要是在路由配置中进行操作。

#### 1、布尔模式

当 `props` 设置为 `true` 时， `route.params` 将被设置为组件的 `props`。

```javascript
const User = {
  template: '<div>User {{$route.params.id}}</div>'
}
const routes = [
  {
    path: '/user/:id',
    component: User
  }
]
```

将上面的代码替换成 `props` 的形式，如下：

```javascript
const User = {
  // 组件中通过 props 获取 id
  props: ['id'],
  template: '<div>User {{id}}</div>'
}

// 路由配置中，增加 props 字段， 并将值设置为 true
const routes = [
  {
    path: '/user/:id',
    component: User,
    props: true
  }
]
```

注意：对于有命名视图的路由，你必须为每个命名视图定义 `props` 配置：

```javascript
const routes = [
  {
    path: '/user/:id',
    components: {
      default: User,
      sidebar: Sidebar
    },
    props:{
      default: true,
      sidebar: false
    }
  }
]
```

#### 2、对象模式

当 `props` 是一个对象时，它将原样设置为组件 `props`。当 props 是静态的时候很有用。

##### 路由配置

```javascript
const routes = [
  {
    path: '/hello',
    component: Hello,
    props: {name: 'World'}
  }
]
```

##### 组件中获取数据

```javascr
const Hello = {
  props: {
    name: {
      type: String,
      default: 'Vue'
    }
  },
  template: '<div>Hello {{ name }}</div>'
}
```

`<Hello />` 组件默认显示 Hello Vue，但路由配置了 `props` 对象，当路由跳转到 `/hello` 时，会显示传递过来的 `name`,页面会显示为 Hello World

#### 3、函数模式

可以创建一个返回 props 的函数。这允许你将参数转换为其他类型，将静态值与基于路由的值相结合等等。

##### 路由配置

使用函数模式时，返回 props 的函数接受的参数为路由记录 `route`。

```javascript
// 创建一个返回 props 的函数
const dynamicPropsFn = route => {
  return {name: route.query.say + "!"}
}

const routes = [
  {
    path: '/hello',
    component: Hello,
    props: dynamicPropsFn
  }
]
```

##### 组件获取数据

当 URL 为 `/hello?say=World` 时，将传递 `{name: 'World!'}` 作为 `props` 传给 `Hello` 组件。

```javascript
const Hello = {
  props: {
    name: {
      type: String,
      default: 'Vue'
    }
  },
  template: '<div>Hello {{ name }}</div>'
}
```

注意：请尽可能保持 `props` 函数为无状态的，因为它只会在路由发生变化时起作用。如果你需要状态来定义 `props`，请使用包装组件，这样 `vue` 才可以对状态变化做出反应。

### 4、其他方式

#### 1、通过 vuex 进行传递

> - store 存储状态
> - A 组件更改 store 中的状态
> - B 组件从 store 中获取

#### 2、通过前端本地存储等方式

> - Local Storage
> - Session Storage
> - IndexedDB
> - Web SQL
> - Cookies

### HTML History 模式

`vue-router` 默认 `hash` 模式 —— 使用 `URL` 的 hash 来模拟一个完整的 `URL`，于是当 `URL` 改变时，页面不会重新加载。

如果不想要很丑的 `hash`，我们可以用路由的 `hiatory` 模式， 这种模式充分利用 `history.pushState` API 来完成 `URL` 跳转而无须重新加载页面。

```javascript
const router = new VueRouter({
  mode: 'history',
  routes: [...]
})
```

当你使用 `history` 模式时， `URL` 就像正常的url，例如 `http://yuorsite.com/user/id`

不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页面客户端应用，如果后台没有正确配置，当用户在浏览器直接访问 `http://yoursite.com/user/id` 就会返回404，这就不好看了。

所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。