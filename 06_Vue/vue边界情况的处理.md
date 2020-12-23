# 处理边界情况

> All the features on this page document the handling of edge  cases，meaning unusual situations that sometimes require bending Vue's  rules a little. Note however, that they all have disadvantages or  situations where they could be dangerous.
>
> 本页的所有功能都记录了边缘情况的处理，这意味着有时需要稍微弯曲Vue规则的异常情况。但是，请注意，它们都有缺点或可能存在危险的情况。

## 1、访问元素&组件

### 1.1、访问根实例 Accessing The Root Instance

通过`this.$root`根实例

```js
// the root Vue instance
new Vue({
    data:{
        foo: 1
    },
    created: function(){
        // 获取 根组件 的数据
        console.log(this.$root.foo)
        // 写入 根组件 的 数据
        this.$root.foo = 2
        // 访问 根组件的 计算属性
        this.$root.bar
    },
    computed:{
        bar: function(){
            alert('我是计算属性Bar，只要有人访问我活着改变我的值，我就执行')
        }
    },
    methods:{
        baz: function(){
            alert('baz')
        }
    }
})
```

这种适合小型代码量的项目使用，中大型项目还是推荐用 `Vuex`来管理应用的状态。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="../vue.js"></script>
    <script src="../vuex.js"></script>
</head>
<body>
<script>
    const store = new Vuex.Store({
        state: {
            foo: 1
        },
        mutations: {
            increment (state) {
                state.foo++
            }
        }
    })
    // The root Vue instance
    new Vue({
        store: store,
        created:function(){
            // 获取根组件的数据
            console.log(this.$store.state.foo); // 1
            // 写入根组件的数据
            this.$store.commit('increment')

            console.log(this.$store.state.foo) // 2
        },
        computed: {
            bar: function () {
                alert('我是计算属性bar，只要有人访问我或者改变我的值，我就执行')
            }
        },
        methods: {
            baz: function () {
                alert('baz')
            }
        }
    })

</script>
</body>
</html>
```

### 1.2、访问父组件实例

> Similar to `$root`, the `$parent` property can be  used to access the parent instance from a child. This can be tempting to reach for as a lazy alternative to passing data with a prop.
>
> 与$root类似，$parent属性可用于从子级访问父实例。作为一种懒散的替代方法，这可能是一种诱人的方法，而不是用道具传递数据。

父组件通过prop向子组件传值，子组件也可以通过`$parent`访问父组件的值

### 1.3、访问子组件或者子元素

通过`$refs`访问子组件。注意：`$refs` 只会在组件渲染完成之后生效。

```html
<div id="app">
    <base-input ref="usernameInput"></base-input>
</div>
```

```js
Vue.component('base-input', {
    template: '<input type="input" ref="input">',
    methods:{
        popUP(){
            alert(111)
        },
        focus: function(){
            this.$refs.input.focus()
        }
    }
})
new Vue({
    el: '#app',
    data: {},
    mounted: function(){
        this.$refs.usernameInput.popUP()
        this.$refs.usernameInput.focus()
    }
})
```

### 1.4、依赖注入

> In fact, you can think of dependency injection as sort of “long-range props”
>
> 事实上，你可以把依赖注入看作是一种“远程道具”

使用 props 是父组件向子组件共享数据，而使用 依赖注入 是父组件向所有子孙组件共享数据（可跨层级的共享数据）

 

```js
// 父组件中 抛出 要分享的 数据
provide: function(){
    return {
        getMap: this.getMap
    }
}

// 子组件中 注入 
inject:['getMap']
```

## 2、程序化的事件监听

- Listen for an event with `$on(event_name, event_handler)`
- Listen for an event only once with `$once(event_name, enent_handler)`
- Stop listening for an event with `$off(event_name, event_handler)`

当需要在一个组件实例上手动侦听事件时，使用。

```html
<div id="app">
    <input ref="dateInput" v-model="date" type="text">
</div>
```

```js
new Vue({
    el: '#app',
    data: {
        date: null
    },
    mounted: function(){
        var picker = new Pikaday({
            field: this.$refs.dateInput,
            format: 'YYYY-MM-DD'
        })
        this.$once('hook:beforeDestory', function(){
            picker.destory()
        })
    }
})
```

## 3、循环引用

### 3.1、递归组件

> Components can recursively invoke themselves in their own template. However, they can only do so with the `name` option.

组件可以在自身模板中调用自己，注意：不要陷入无限循环。

```html
<div>
    <base-input />
</div>
```

```js
Vue.component('base-input', {
    name: 'stack-overflow',
    template: `<div> <stack-overflow /> </div>`
})
new Vue({
    el: '#app',
    data: {}
})
```

### 3.2、组件之间的循环引用

常见场景：渲染多层级结构时会用到。

## 4、