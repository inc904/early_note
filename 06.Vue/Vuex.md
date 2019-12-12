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
		// this.$store.commit('方法名称'， '按需传入唯一参数')
	},
	getters:{
		// this.$store.getters.***
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