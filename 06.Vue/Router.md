## 什么是路由
1. 后端路由
	对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源。
2. 前端路由
	对于单页面应用程序，主要通过URL中的 hash 来实现不同页面之间的切换，同时，hash 有一个特点：
	HTTP 请求中不会包含 hash 相关的内容，单页面程序中的页面的跳转，主要用 hash 跳转。
3. 在单页面中这种通过 hash 变切换页面的方式，叫做前端路由（区别于后端路由）。

## 在 Vue 中使用 Vue-router
### 步骤
	1.定义组件模板对象
	2.注册组件
	3.定义路由规则
	4.注册 Vue 实例

### 路由配置
功能：

	1. 定义路由匹配
	2. 配置 router-link 激活类名
代码：
```js
new Router({
	routers: [
		{ path: '/', redirect: login}
		{ path: '/login', component: login}
	],
	linkAcitveClass: 'my-router-link-active'
})
```
### router-link
```js
/**
* 高亮当前选中 link
* 选中时使用的类名：
* router-link-active  
* 激活时使用的类名，默认值可以可以使用路由的构造选项 linkActiveClass 来全局配置：
* router-link-exact-active
* 是否激活
*/
```

### 路由传参
两种方式
- 第一种：query
```html
<!-- HTML代码 -->
<router-link to='/login?id=07&name=zch'>登录</router-link>
```
```js
// js代码
{ path: '/login', component: login},
```
- 第二种：params
```html
<!-- HTML代码 -->
<router-link to='/login/09/ls'>登录</router-link>
```
```js
// js代码
{ path: '/login/:id/:name', component: login},
```
### 命名路由



### 嵌套路由

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

### 路由高亮

#### active-class

默认值：“router-link-active”

设置链接激活时使用的CSS类名。默认值可以通过路由的构造选项`linkActiveClass`来全局配置。

#### 第一种方式：使用vue内置的属性

```css
.router-link-active{
    font-size: 32px;
    color: red;
}
```

#### 第二种方式：自定义样式

在新建的路由对象内部设置`linkActiveClss`属性，该属性和`routes`属性平级

`linkActiveClass: 'myActive'`

```css
.myActive{
    font-size: 32px;
    color: red;
}
```

