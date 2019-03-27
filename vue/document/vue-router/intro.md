### 1.Vue-Router 

----
`用 Vue.js + Vue Router 创建单页应用，是非常简单的 首先你需要下载它！引入它 使用它`

> 1.先创建组件

> 2.再说明路由

> 3.再创建路由控制器

> 4.再路由注入

```javascript
var homeComponent = {
    template:`
        <div class="panel">
            <div>你们好啊！ 这是系统主页</div>  
        </div>
    `
}

var newsComponent = {
    template:`
        <div class="panel">
            <div>你们好啊！ 这是新闻页面</div>  
        </div>
    `
}

const routes = [
    {path:"/home",component:homeComponent},
    {path:"/news",component:newsComponent}
]

const router = new VueRouter({
    routes
})

var demo = new Vue({
    el:"#demo",
    router //注入路由
});
```

### 2.路由的模式
`vue-router 默认 hash 模式 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。`

```
http://127.0.0.1/Index.html#/news
```

> `如果不想要很丑的 hash，我们可以用路由的 history 模式，这种模式充分利用 history.pushState API 来完成 URL 跳转而无须重新加载页面。当你使用 history 模式时，URL 就像正常的 url 不过这种模式要玩好，还需要后台配置支持。`

> `因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 http://oursite.com/user/id 就会返回 404，这就不好看了。所以呢，你要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 index.html 页面，这个页面就是你 app 依赖的页面。`


### 3.动态路由匹配 例子: nesting.html

```javascript
const User = {
  template: '<div>User {{ $route.params.id }}<</div>'
}

const router = new VueRouter({
  routes: [
    // 动态路径参数 以冒号开头
    { path: '/user/:id', component: User }
  ]
})

```


|模式 |	匹配路径 |	$route.params|
|:----|:----|:----|
|/user/:username |	/user/evan |	{ username: 'evan' }|
|/user/:username/post/:post_id |	/user/evan/post/123 |	{ username: 'evan', post_id: '123' }|

##### 3.1 响应路由参数的变化
`提醒一下，当使用路由参数时，例如从 /user/foo 导航到 /user/bar，原来的组件实例会被复用。因为两个路由都渲染同个组件，比起销毁再创建，复用则显得更加高效。不过，这也意味着组件的生命周期钩子不会再被调用。`

复用组件时，想对路由参数的变化作出响应的话，你可以简单地 watch (监测变化) $route 对象：
```javascript
const User = {
  template: '...',
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
}

```

##### 3.2 路由匹配
`捕获所有路由或 404 Not found 路由 常规参数只会匹配被 / 分隔的 URL 片段中的字符。如果想匹配任意路径，我们可以使用通配符 (*)：`

```javascript
{
  // 会匹配所有路径 写在所有的路由的最下面 做404 页面
  path: '*'
}
{
  // 会匹配以 `/user-` 开头的任意路径
  path: '/user-*'
}

```
`当使用通配符路由时，请确保路由的顺序是正确的，也就是说含有通配符的路由应该放在最后。路由 { path: '*' } 通常用于客户端 404 错误。如果你使用了History 模式，请确保正确配置你的服务器。`

`https://github.com/pillarjs/path-to-regexp`  `vue的路由匹配就是依据这个 path-to-regexp`


### 4.嵌套路由  例子:nesting.html
`要在嵌套的出口中渲染组件，需要在 VueRouter 的参数中使用 children 配置：`

```javascript
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User,
      children: [
        {
          // 当 /user/:id/profile 匹配成功，
          // UserProfile 会被渲染在 User 的 <router-view> 中
          path: 'profile',
          component: UserProfile
        },
        {
          // 当 /user/:id/posts 匹配成功
          // UserPosts 会被渲染在 User 的 <router-view> 中
          path: 'posts',
          component: UserPosts
        }
      ]
    }
  ]
})
```

### 5.编程式的导航
`除了使用 <router-link> 创建 a 标签来定义导航链接，我们还可以借助 router 的实例方法，通过编写代码来实现。`

`router.push(location, onComplete?, onAbort?)`

注意：在 Vue 实例内部，你可以通过 $router 访问路由实例。因此你可以调用 this.$router.push。

想要导航到不同的 URL，则使用 router.push 方法。这个方法会向 history 栈添加一个新的记录，所以，当用户点击浏览器后退按钮时，则回到之前的 URL。

当你点击 `<router-link>` 时，这个方法会在内部调用，所以说，点击 `<router-link :to="...">`等同于调用 router.push(...)。

|声明式|编程式|
|----|---|
|`<router-link :to="...">`|router.push(...)|

该方法的参数可以是一个字符串路径，或者一个描述地址的对象。例如：

```javascript
// 字符串
router.push('home')

// 对象
router.push({ path: 'home' })

// 命名的路由
router.push({ name: 'user', params: { userId: '123' }})

// 带查询参数，变成 /register?plan=private
router.push({ path: 'register', query: { plan: 'private' }})

```

注意：如果提供了 path，params 会被忽略，上述例子中的 query 并不属于这种情况。取而代之的是下面例子的做法，你需要提供路由的 name 或手写完整的带有参数的 path：

```javascript
const userId = '123'

router.push({ name: 'user', params: { userId }}) // -> /user/123
router.push({ path: `/user/${userId}` }) // -> /user/123
// 这里的 params 不生效
router.push({ path: '/user', params: { userId }}) // -> /user
```

在 2.2.0+，可选的在 router.push 或 router.replace 中提供 onComplete 和 onAbort 回调作为第二个和第三个参数。这些回调将会在导航成功完成 (在所有的异步钩子被解析之后) 或终止 (导航到相同的路由、或在当前导航完成之前导航到另一个不同的路由) 的时候进行相应的调用。


`router.replace(location, onComplete?, onAbort?)`

跟 router.push 很像，唯一的不同就是，它不会向 history 添加新记录，而是跟它的方法名一样 —— 替换掉当前的 history 记录。


|声明式| 	编程式|
|:----|:----|
|`<router-link :to="..." replace>`| `router.replace(...)`|



`router.go(n)`  

这个方法的参数是一个整数，意思是在 history 记录中向前或者后退多少步，类似 window.history.go(n)。

```javascript
// 在浏览器记录中前进一步，等同于 history.forward()
router.go(1)

// 后退一步记录，等同于 history.back()
router.go(-1)

// 前进 3 步记录
router.go(3)

// 如果 history 记录不够用，那就默默地失败呗
router.go(-100)
router.go(100)

```

`操作 History`

`你也许注意到 router.push、 router.replace 和 router.go 跟 window.history.pushState、 window.history.replaceState 和 window.history.go
好像， 实际上它们确实是效仿 window.history API 的。`


### 6.命名视图
时候想同时 (同级) 展示多个视图，而不是嵌套展示，例如创建一个布局，有 sidebar (侧导航) 和 main (主内容) 两个视图，这个时候命名视图就派上用场了。你可以在界面中拥有多个单独命名的视图，而不是只有一个单独的出口。如果 router-view 没有设置名字，那么默认为 default。


```html
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>

```

一个视图使用一个组件渲染，因此对于同个路由，多个视图就需要多个组件。确保正确使用 components 配置 (带上 s)：

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
})

```

### 7.重定向和别名
`重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b：`

```javascript
//重定向也是通过 routes 配置来完成，下面例子是从 /a 重定向到 /b：
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: '/b' }
  ]
})

//重定向的目标也可以是一个命名的路由：
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: { name: 'foo' }}
  ]
})

//甚至是一个方法，动态返回重定向目标
const router = new VueRouter({
  routes: [
    { path: '/a', redirect: to => {
      // 方法接收 目标路由 作为参数
      // return 重定向的 字符串路径/路径对象
    }}
  ]
})

```

#### 7.2 别名
`/a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样。`
```javascript
const router = new VueRouter({
  routes: [
    { path: '/a', component: A, alias: '/b' }
  ]
})

```

### 8.路由组件传参
`在组件中使用 $route 会使之与其对应路由形成高度耦合，从而使组件只能在某些特定的 URL 上使用，限制了其灵活性。
使用 props 将组件和路由解耦：`

```javascript
const User = {
  props: ['id'],
  template: '<div>User {{ id }}</div>'
}
const router = new VueRouter({
  routes: [
    { path: '/user/:id', component: User, props: true },

    // 对于包含命名视图的路由，你必须分别为每个命名视图添加 `props` 选项：
    {
      path: '/user/:id',
      components: { default: User, sidebar: Sidebar },
      props: { default: true, sidebar: false }
    }
  ]
})

```

##### 1.配置信息

> `tag`:`决定将 link 渲染成什么标签`

```html
<router-link to="/user/login" tag="div">登录</router-link>
```

`RouteConfig` 的类型定义：
```javascript
declare type RouteConfig = {
  path: string;  //路径
  component?: Component; //绑定那个组件
  name?: string; // 命名路由
  components?: { [name: string]: Component }; // 命名视图组件
  redirect?: string | Location | Function;
  props?: boolean | Object | Function; //是否允许props 传值
  alias?: string | Array<string>; //路由别名
  children?: Array<RouteConfig>; // 嵌套路由
  beforeEnter?: (to: Route, from: Route, next: Function) => void;
  meta?: any;

  // 2.6.0+
  caseSensitive?: boolean; // 匹配规则是否大小写敏感？(默认值：false)
  pathToRegexpOptions?: Object; // 编译正则的选项
}
```
`router` 的类型定义

```c#
beforeRouteEnter (to, from, next) {
  next(vm => {
    // 通过 `vm` 访问组件实例
  })
}

```
