

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

  直接删除元素

- v-show

  控制样式 的显隐

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





## 插槽

### 普通插槽：

```js
  Vue.component('AlertBox', {
      template: `
        <div class="demo-alert-box">
        	<strong>普通插槽：Error!</strong>
	        <slot></slot>
        </div>
		`
  })
```

```html
 <alert-box>
     Something bad happened.
</alert-box>
<!-- 普通插槽：Error! Something bad happened. -->
```

### 具名插槽：

```js
    Vue.component('success-box', {
        template: `
          <div class="demo-alert-box">
            <strong>具名插槽：success!</strong>
            <p>
              成功：              
              <slot name="success" />
            </p>
            <p>
              下一步：
              <slot name="main" />
            </p>
          </div>
        `
      })
```

```html

 <success-box>
     <template v-slot:success>
         <!-- 命名缩写   <template #success> -->
        <p>
             everything is ok !
         </p>
        
     </template>
     
     <!-- 插槽缩写 
         <p slot="success">
             everything is ok !
         </p>
      -->
     
     <template v-slot:main>
         go for a breast。
     </template>
</success-box>
<!-- 
具名插槽：success!
成功： everything is ok !

下一步： go for a breast。
-->
```

### 作用域插槽

```js
   Vue.component('info-box', {
        data: () => {
          return {
            student: {
              name: 'jax',
              age: 13
            }
          }
        },
        template: `
          <div class="demo-alert-box">
            <strong> 作用域插槽：infomation:</strong>
            <slot name="info" :student="student"></slot> // 将组件上的实例属性作为属性传递给插槽
          </div>
        `
      })
```



```html
 <info-box>
        <template v-slot:info="student"> // 在插槽上的属性 成为 插槽Prop，使用带值得 v-slot 定义 prop 得名字
          <p>
            school: {{school.name}} // 可以直接访问父组件上的实例属性
          </p>
          <p>
            name:{{student.student.name}}
          </p>
          <p>
            age:{{student.student.age}}
          </p>
        </template>
      </info-box>


<!-- 
作用域插槽：infomation:
school: 清华

name:jax

age:13
-->
```

1. 当只有默认插槽得时候，v-slot:default="somethin" 缩写  v-solt="something"
2. 默认插槽得缩写语法不能和具名插槽混用
3. 只要出现多个插槽，必须为所有得插槽命名

##### 解构prop

```html
 <info-box>
<!-- 解构前 <template v-slot:info="student"> -->
     <template v-slot:info="{student}">
     
         <p>
             <-解构prop->
                 </p>
         <p>
             school: {{school.name}}
         </p>
         <p>
<!--解构前    name:{{student.student.name}} -->
             name:{{student.name}}
             
         </p>
         <p>
             age:{{student.age}}
         </p>
     </template>
</info-box>
```



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



