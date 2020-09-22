## 组件

### 组件化和模块化

- 模块化： 基于代码逻辑的角度来划分的
- 组件化： 基于UI界面的角度来划分的

### 全局组件

#### 定义组件的三种方式

1.使用`Vue.extend`配合`Vue.component`

```js
# 第一种方式
// 1. 创建一个全局组件
var login = Vue.extend({
    template: '<h1>登录</h1>'
})
// 2. 注册组件
// Vue.component('组件的名称', 模板对象)
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

2. pasclaCase

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
// 使用
// <login></login>
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

