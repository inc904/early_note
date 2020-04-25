### 路由基本概念

1. 后端路由：对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源。
2. 前端路由：对于单页面应用，只要通过URL中的hash（#号）来实现不同页面之间的切换，同时hash有一个特点：HTTP请求中不会包含hash相关的内容；
3. 在单页面应用程序中，这种通过hash改变切换页面的方式，乘坐前端路由（区别于后端路由）

### 

### 在 Vue 中使用 vue-router

1. 导入 vue-router 组件类库 js文件
2. 使用 router-link 组件来导航

```html
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
```

1. 使用 router-view组件来显示匹配到的组件

```html
<!-- to="/login" -->
<router-view>
    <!-- 显示登录组件的内容 -->
<router-view>
```

```js
// 路由组件的配置和匹配规则
new Vue({
    router: new VueRouter({ // 路由对象实例
            routes: [ // 路由匹配规则
                { path: '/', redirect: '/login' }, // 默认路由定义
                { path: '/login', component: login },
                { path: '/register', component: register },
            ],
            linkActiveClass: 'my-active', // 自定义链接激活时候的类名
        }),
})
```

#### 在路由规则中定义参数

1. query方式传参
2. params方式传参

```html
<div id="app">
        <h1>Hello App!</h1>
        <p>
            <!-- 使用 query 方式传参 不需要修改 路由规则 中的 path 属性 -->
            <router-link to="/login?id=10&name=zzc" tag="a" name="lllogin">登录</router-link>
            <!-- 使用params方式传参 -->
            <router-link to="/register/12/whh">注册</router-link>
        </p>
        <router-view></router-view>
    </div>
<scritp>
// js 代码
</script>

```

```js
// js 代码
new Vue({
    router: new VueRouter({ // 路由对象实例
        routes: [ // 路由匹配规则
            { path: '/', redirect: '/login' },
            { path: '/login', component: login, name: 'ytf' }, // query 方式传参，不需要修改匹配规则
            { path: '/register/:id/:name', component: register }, // params 传参，需要 定义 匹配规则
        ],
    }),
})
<!-- 
    参数传递后，可以在各自的组件定义中，在 created 钩子函数中 拿到：
    1. this.$route.query.id
    2. this.$route.params.id
 -->
```



### vue-router 的嵌套路由

```js
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

### vue-router  动态路由匹配

```html
    <router-link to="/user/1">user1</router-link>
    <router-link to="/user/2">user2</router-link>
    <router-link to="/user/3">user3</router-link>


```

```js
// 父组件中 动态路由匹配
var router = new VueRouter({
    routes: [
        // 动态路径参数，以冒号开头，占位符
        { path: '/user/:id', component: User }
    ]
})
```



```js
// 匹配到的页面中
{{$route.params.id}} 得到 传递的 id 参数
```

#### 路由组件传递参数

$route与对应路由形成高度耦合，不够灵活，所以可以使用 props 将组件和路由解耦

```js
const user = new VueRouter({
    routes: [
        // case 1. props 的值 为 布尔类型
        {path:'/user/:id', components: User, props: true}
        // case 2 ： props 的值 为对象属性
         {path:'/user/:id', components: User, props: {uname: 'tomy', id: '12'}}
        // case 3: props 的值 为 函数类型
        {path:'/user/:id', components: User,props: route => ({uname: 'tomy', age: '12', id: route.params.id })
}
                           
    ]
})
// 对应的路由组件中
const User = {
    props: ['id'] //  case 1 ： 使用 props 接收 路由参数
    props: ['uname', 'age'] // case 2 : 接收对象形式的 props
    props: ['uname', 'age', 'id'] // case 3 : 接收函数形式的 props
    
    template: '<div>ID: {{id}}</div>' // 使用路由参数
}
```

### vue-router 命名路由

```js
var router = new VueRouter({
    routes: [
        // 动态路径参数，以冒号开头，占位符
        { path: '/user/:id', component: User, name: 'user' }
    ]
})

<route>
```

```html
 <router-link to="/user/1">user1</router-link>

<route-link :to="{name: 'user',params: {id: 007}}">User</route-link>
```




### vue-router 编程式导航

##### router.push(location)

```js
router.push({name: 'user', params: {id: 007} } )
```

##### router.go(n)

##### router.replace()

### 路由守卫

#### 全局守卫

- beforeEach(to, from, next){ } 前置守卫
- afterEach(to, from){ } 后置守卫

### 组件内得守卫

在路由组件内直接定义。

- beforeRouteEnter(to, from, next){ }
- beforeRouteUpdate(to, from, next){ }
- beforeRouteLeave(to, from, next){ }

### 组件独享得守卫

在路由配置上定义守卫

- beforeEnter(to, from, next){ }