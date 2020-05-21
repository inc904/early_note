##### 问题

> 最近些日子项目中突然碰到了一个需求，再完成编辑操作之后需要进行页面刷新，通过实验有如下几种姿势可以解决需求中的问题，下面进行简单总结如下。

##### 姿势一：`this.$router.go(0)`

> 这个姿势是利用了 history 中前进和后退的功能，传入 0 刷新当前页面。但是有一个问题就是页面整个刷新过程中会白屏，严重影响用户的体验感，效果不好。
>
> 
>
> ```kotlin
> this.$router.go(0)
> ```

##### 姿势二：`location.reload()`

> 这个姿势是利用了直接使用刷新当前页面的方法。但是同样存在有一个问题就是页面整个刷新过程中会白屏，严重影响用户的体验感，效果也是不好，和姿势一的现象一直，也不推荐使用。
>
> 
>
> ```css
> location.reload()
> ```

##### 姿势三：`provide / inject组合`

> 允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在起上下游关系成立的时间里始终生效。
>  `provide：`选项应该是一个对象或返回一个对象的函数。该对象包含可注入其子孙的属性。
>  `inject：`一个字符串数组，或一个对象，对象的 key 是本地的绑定名。
>  注意：provide和inject绑定并不是可响应的。这是刻意为之的。如果你传入了一个可监听的对象，那么其对象的属性还是可响应的。
>  基本使用步骤如下：
>
> - 步骤一：（App.vue）
>    通过 $nextTick()，协助实现。先把 <router-view /> 移除，移除后再重新添加，达到刷新当前页面的功能。是目前最合适的实现方式。
>
> 
>
> ```vue
> <template>
>  <div id="app">
>    <router-view v-if="isRouterAlive"/>
>  </div>
> </template>
> 
> <script>
> export default {
>  name: 'App',
>  provide () {
>    return{
>      reload: this.reload
>    }
>  },
>  data() {
>    return {
>        isRouterAlive: true
>    }
>  },
>  methods:{
>    reload(){
>      this.isRouterAlive = false
>      this.$nextTick(function(){
>        this.isRouterAlive = true
>      })
>    }
>  }
> }
> </script>
> ```
>
> - 步骤二：（chapter.vue）
>
> 
>
> ```bash
> inject: ['reload'],
> ```
>
> ![img](https:////upload-images.jianshu.io/upload_images/13331500-9fb14285c3b5cf01.png?imageMogr2/auto-orient/strip|imageView2/2/w/568/format/webp)
>
> 代码结构
>
> - 步骤三：（chapter.vue）
>    直接this.reload()调用，即可刷新当前页面。
>
> 
>
> ```kotlin
> this.reload()// 需要刷新页面
> ```
>
> ![img](https:////upload-images.jianshu.io/upload_images/13331500-5a1f36d61cefe074.png?imageMogr2/auto-orient/strip|imageView2/2/w/554/format/webp)
>
> 代码结构

##### 结束语

> 到此问题解决，不多说了，抽根烟，解心宽，继续写代码了....



作者：清水三千尺
链接：https://www.jianshu.com/p/91a3bd6060c4
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。