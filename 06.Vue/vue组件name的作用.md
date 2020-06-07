写 vue 文件的时候，会给组件命名

```js
export default {
    name: 'xxx',
    data(){
        return {}
    }
}
```

### 当项目使用 keep-alive 组件时，可搭配组件 name 进行缓存过滤。

```js
export default{
    name: 'Detail'

    mounted(){
    
	},
    methods:{
        getInfo(){
            axios.get('xx/detail.json',{
                params:{
                    id: this.$route.params.id
                }
            }).then(this.getInfoSucc)
    }
},
```

以为我们再 App.vue 中使用了 Keep-alive 导致我们第二次进入的时候页面不会重新请i去，即触发 mounted 函数。有两种解决方法，一个是增加一个 activated() 函数，每次i进入页面的时候再获取一次数据。

还有一个方案就是在 keep-alive 中增加一个过滤：

```vue
<div id="app">
    <keep-alive exclude="Detali">
    	<router-view />
    </keep-alive>
</div>
```

### DOM 做递归组件时

比如说 detail.vue 组件里 有一个 list.vue 组件，递归迭代时需要调用自身 name

```vue
// list.vue
<div>
    <div v-for="(item,index) of list" :key="index">
      <div>
        <span class="item-title-icon"></span>
        {{item.title}}
      </div>
      <div v-if="item.children" >
        <detail-list :list="item.children"></detail-list>
      </div>
    </div>
 </div>
<script>
export default {
  name:'DetailList',//递归组件是指组件自身调用自身
  props:{
    list:Array
  }
}
</script>
```

```js
// list 数据
const list = [{
     "title": "A",
     "children": [{
      "title": "A-A",
      "children": [{
       "title": "A-A-A"
      }]
     },{
        "title": "A-B"
     }]
    }, {
     "title": "B"
    }, {
     "title": "C"
    }, {
     "title": "D"
    }]
```



![img](https://img.jbzj.com/file_images/article/201805/2018523154853255.png?2018423154929)

### 在使用 vue-devtool 时

vue-devtool 调试工具里显示的组件名称时由 vue 中的组件 name 决定的![img](https://img.jbzj.com/file_images/article/201805/2018523154947762.png?201842315502)