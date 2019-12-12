## 定义Vue组件

### 组件化和模块化
- 模块化： 基于代码逻辑的角度来划分的
- 组件化： 基于UI界面的角度来划分的

## 全局组件
```js
# 第一种方式
// 1. 创建一个全局组件
var tpl = Vue.extend({
	template: '<h3>Vue.extend 创建的 h3 全局 Vue 组件</h3>'
})
// 2. 注册组件
// Vue.component('组件的名称', 模板对象)
Vue.component('myCom', tpl)

//3. 使用
// <my-com></my-com>

# 第二种
// 第一步，第二步
Vue.component('myCom', Vue.extend({
	template: '<h3>Vue.extend 创建的 h3 全局 Vue 组件</h3>'
}))
// 第三步 使用

# 第三种
// 1，2 创建，注册
Vue.component('mycom', {
	data: function(){
		return {}
	},
	template: '<h3>Vue.extend 创建的 h3 全局 Vue 组件</h3>'
})

// 3.使用
````

## 私有组件
```js
// 定义
new Vue({
	components:{
		login: {
			template: '<h1>私有login组件</h1>'
		}
	}
})
// 使用
// <login></login>
```