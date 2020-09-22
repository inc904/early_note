## Vuex 是什么

vue的`状态管理模式`；
集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化；

## 使用

1. 安装
` npm i vuex -D `
2. 配置
```js
// 注册
import Vuex from 'vuex'
Vue.use(Vuex)
// 创建 store
var store = new Vuex.store({
	state: {
		// 调用方式： this.$store.state.***
	},
	mutations: {
		// 组件中调用：this.$store.commit('方法名称'， '按需传入唯一参数')
	},
	getters:{
		// 调用方式：this.$store.getters.***
	}
})
// 挂载
var vm = new Vue({
	el: "#demo"
	data: {}
	router,
	store
})
```