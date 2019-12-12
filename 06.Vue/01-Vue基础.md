## Vue 实例

```js
let vm = new Vue({
  el: '#app', // 挂载对象
  data: {}, // 绑定数据
  methods: {} // 自定义调用的方法
})
```

## 模板语法

### 插值

- {{ 插值表达式 }}  `{{ message }} `

   数据绑定 。mustache 语法中的数据解析为 普通文本

  语句中支持 JavaScript 表达式，不支持 语句 和 流控制

### 指令
- v-html  文本输入，可以输出 普通文本， 可以输出 HTML
- v-text  文本输入
- v-clock meiyou
- v-bind  属性绑定  `v-bind:title='myTitle'` 简写 `:title='myTitle'`
- v-on:   事件监听 `v-on:click='myClick'` 简写 `@click='myClick'`
- v-for   循环
- v-if & v-show  条件渲染
  v-if    直接删除元素
  v-show  通过 display 控制，频繁切换的时候使用
- v-model 双向数据绑定
- v-cloak 利用样式来处理未编译的差值表达式 `*[v-cloak]: { display; none; }`

#### 自定义指令

##### 自定义 全局指令`focus`

```js
Vue.directive('focus', {
  // 在每个函数中，第一个参数都是 el ，表示绑定指令的那个元素，是一个原生的js对象
  // binding 可以拿到 自定义指令 传的值
  bind: function(el, binding){
  	// 指令已绑定到元素上的时候，就会执行，只执行一次  
  },
  inserted(el){
    // 标识元素插入到 DOM 中的时候，会执行，只触发一次
    el.focus()
  },
  updated: function(){
    // 当 VNode 更新的时候，会执行，可能会触发多次
  }
})

# 参数1：是指令的 名称，定义的时候不需要'v-'前缀，使用的时候必须加前缀

# 参数2： 是一个对象，对象身上有指令相关的处理函数（钩子函数），在特定的阶段执行特定的操作

# 简写形式

```
##### 私有指令

```js
directives: {
  'FontWeight': { // 字体加粗
    bind: function(el,binding){
      el.style.fontWeight = binding.value
    }
  }
}
```
- 钩子函数：

一个自定义对象可以有以下几个钩子函数：

```js
bind
inserted
update
componentUpdated
unbind
```

自定义全局指令的时候，必须定义在vue实例前面
如果自定义指令需要在bind和update阶段触发相同行为，而不关心其他钩子，第二个参数可以简写为function，不用写 {}

   

### methods

定义组件使用到的方法

### 过滤器

用于常见的文本格式化。仅可用在 mustache 插值和 v-bind 表达式中。

```html
<td>{{ date | dateFormat() }}</td>
```

#### 公有过滤器

定义在 vue 上，任何 vue 实例都可以使用。

```js
Vue.filter('dateFormat', function(){
    // code...
})
```



#### 私有过滤器

```js

```



## 计算属性和监听器
1. `cpmouted`属性的结果会被缓存，除非依赖的响应属性变化才会被重新计算，主要当做计算属性使用。
2. `methods`表示一个具体的操作，主要用来书写业务逻辑。
3. `watch`一个对象，键是对应的回调函数，主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑，
    可以看做是`computed`和`methods`的结合体。



## Class 和 Style 绑定

### 绑定 HTML Class

#### 对象语法

`v-bind:class='Object'` 动态的切换 class

```html
<div class="static" v-bind:class="{{ active: isActive, text-danger: hasError }}"></div>
```

```js
data: {
  isActive: true,
  hasError: false
}
```

结果：

```html
<div class="static active">
  
</div>
```



#### 数组语法

`v-bind:class='Array'`

#### 用在组件上 

### 绑定内联样式

`v-bind:style=''`

属性值需要用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名

## 条件渲染

- v-if
- v-show

## 列表渲染

### v-for 循环

1. 迭代数组  `v-for = "item, index in Array"`
2. 迭代对象  `v-for = "val, key in JSON"`
3. 迭代字符串  `v-for = "char, index in String"`
4. 迭代数字 `v-for =  "i in Number"`

### :key 属性

key 属性只能使用 Number/String 

2.2+ 版本，在组件渲染列表，必须加 key 属性

### 虚拟DOM 

类JSON对象



## 事件处理

### v-on

### 事件修饰符

- .stop   阻止冒泡
- .prevent  阻止默认事件
- .native  原生事件，组件中使用
- .capture
- .self
- .once  事件只触发一次
- .keyCode 键盘事件

### 键值修饰符

自定义键码与键名字

`Vue.config.keycode = Number`

```html
<input ctime="text" v-model="brand" @keyup.enter="add">
<input ctime="text" v-model="brand" @keyup.f2="add">
<input ctime="text" v-model="brand" @keyup.113="add">
```

```js
 Vue.config.keyCodes.f2 = 113 
```



### 表单输入绑定

- v-model

## vue 实例的生命周期

生命周期事件，生命周期函数

- 创建时期

  - beforeCreate
  - created
  - beforeMounted
  - mounted

- 运行时期

  - beforeUpdate
  - updated

- 销毁时期

  - beforeDestory

  - destoryed

    

## 过渡 & 动画

两个动作 => Enter & Leave

- Enter动作，属于 v-enter-active 阶段
  - v-enter
  - v-enter-to
- Leave， v-leave-active 阶段
  - v-leave
  - v-leave-to

`v-` 属于动画前缀，可自定义，` name="name" ` 指定的name即为前缀

除了使用默认类名写自定义样式， 还可以 自定义 enter 和 leave 的类名， 以此借助第三方的样式

```html
<transition
    name="custom-classes-transition" // 自定义前缀，动画名称
    enter-active-class="animated tada" // 自定义类名
    leave-active-class="animated bounceOutRight" // 自定义
    :duration="1000" // 过度持续时间
    mode="out-in" // 过度模式 in-out & out-in

    // 动画过程中的 JavaScript 钩子：
    v-on:before-enter="beforeEnter"
    v-on:enter="enter"
    v-on:after-enter="afterEnter"
    v-on:enter-cancelled="enterCancelled"

    v-on:before-leave="beforeLeave"
    v-on:leave="leave"
    v-on:after-leave="afterLeave"
    v-on:leave-cancelled="leaveCancelled"
>
    // code...
</transition>
```

`<transition> `标签 内部只能有一个子元素
`<transiton-group> `可以进行列表过度

### 动画过程中的钩子函数：

```js
methods: {
    beforeEnter: function (el) {
    // ...
    },
    // 当与 CSS 结合使用时
    // 回调函数 done 是可选的
    enter: function (el, done) {
        // ...
        done()
    },
    afterEnter: function (el) {
        // ...
    },
    enterCancelled: function (el) {
        // ...
    },
    // --------
    // 离开时
    // --------
    beforeLeave: function (el) {
        // ...
    },
    // 当与 CSS 结合使用时
    // 回调函数 done 是可选的
    leave: function (el, done) {
        // ...
        done()
    },
    afterLeave: function (el) {
        // ...
    },
    // leaveCancelled 只用于 v-show 中
    leaveCancelled: function (el) {
        // ...
    }
}

```



## 组件

组件化：UI模块的角度。

模块化：代码逻辑的角度。

### 定义组件的三种方式

1.使用`Vue.extend`配合`Vue.component`

```js
var login = Vue.extend({
    template: '<h1>登录</h1>'
})
Vue.component('login', login)
```

2. 使用 Vue.component

```js
Vue.component('resgister',{
    template: '<h1>注册</h1>'
})
```

3. 将模板字符串定义到 script 标签中

```html
<script id="tmpl" type="x-template">
    <div> <a>登录</a> | <a>注册</a> </div>
</script>
```

同时使用 Vue.component 来定义组件

```js
Vue.component('account', {
    template: '#tmpl'
})
```

### 组件名大小写

1. kebab-case

```js
Vue.component('my-component-name', { /* ... */ })
```

引用组件的使用也必须使用 `<my-component-name>`

1. pasclaCase

```js
Vue.component('MyComponentName', { /* ... */ })
```

引用组件的时候，两种方式都可以。`<my-component-name>` 和 `MyComponentName`

### 局部组件

```js
var login =  {
    template: '<h1>登录</h1>'
}
new Vue({
    el: '#app',
    methos:{},
    components: {
        login: 'login',
        register
    }
})

```

### 组件传值

#### 父组件给子组件传值 props

1. 在父组件中定义好数据
2. 组件调用的时候，使用自定义属性的方式接收
3. 在子组件的注册中，使用`props:['sth']` 接收
4. 之后可以在子组件的内容中调用传来的数据值

#### 子组件调用父组件的方法

1. 在父组件中定义好的方法
2. 在实例中使用的组件标签中，接受事件，形式如下 `<cmt @func="parentFun"></cmt>`；
   接收的事件名（func）可自定义，值为父组件中的方法名；
   自定义方法名字的时候，不能使用驼峰命名法，可以使用全小写或者肉串命名法。
3. 在子组件得模板内容中，设置 普通的 触发事件A  
4. 接收完成后，在子组件的方法A中使用`this.$emit('func')`调用

#### 获取DOM和组件引用

```html
<p refs="id">test text</p>
<cmt refs="cmt"></cmt>
```

```js
this.$refs.Selector // 用法示例
this.$refs.id.innnerText // => <p>--> test text
this.$refs.cmt.message // => <cmt> --> data->message 获取子组件上的data
this.$refs.cmt.show() // => <cmt> --> methods-> show() 获取子组件上的 methods 中定义的 方法
```

## 路由

1. 后端路由：对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源。
2. 前端路由：对于单页面应用，只要通过URL中的hash（#号）来实现不同页面之间的切换，同时hash有一个特点：HTTP请求中不会包含hash相关的内容；
3. 在单页面应用程序中，这种通过hash改变切换页面的方式，乘坐前端路由（区别于后端路由）

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
new Vue({
    router: new VueRouter({ // 路由对象实例
        routes: [ // 路由匹配规则
            { path: '/', redirect: '/login' },
            { path: '/login', component: login, name: 'ytf' }, // query 方式传参，不需要修改匹配规则
            { path: '/register/:id/:name', component: register }, // params 传参，需要 定义 匹配规则
        ],
    }),
})
</script>
<!-- 
    参数传递后，可以在各自的组件定义中，在 created 钩子函数中 拿到：
    1. this.$route.query.id
    2. this.$route.params.id
 -->
```

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

### 命名路由