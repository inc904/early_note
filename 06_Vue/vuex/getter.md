## Getter 

### 概念：

Getter 用于 对 Store 中的数据进行加工处理形成新的数据。

 不修改 store 中的原数据，只起到包装数据的作用。

1. getter 可以对 Store 中已有的数据进行加工处理之后形成新的数据，类似 Vue 中的计算属性。

2. Store 中的数据 发生变化，getter 的数据也会跟着变化。


### 定义 getters
```js
state: {
	todos:{
		{id:1, text:'111', done: true},
		{id:2, text:'222', done: false}
	}
}
getters:{
	doneToods: state =>{ // 普通的getter，类似计算属性
		return state.todos.filter(todo => todo.done)
	}
	getTodoById:(state) => (id) =>{ 
	//  通过给 getter返回一个函数，来实现给 getter 传参
		return state.todos.find(todo => todo.id === id )
	}

	// 高阶函数的形式：两个连续的 箭头函数，如上
	get(state){
		return function(id){
			return todo.id === id
		}
	}
}
```
[js 中的多个连续的箭头函数与柯里化](https://zhuanlan.zhihu.com/p/26794822)

高阶函数定义：将函数作为参数或者返回值是函数的函数。
[06_Vue/vuex/getter.md](06_Vue/vuex/getter.md)
### 使用方式：

第一种方式：通过方法访问

```js
this.$store.getters.xxx
```
> getter 在通过方法访问时，每次都会去进行调用，而不会缓存结果。

第二种方式： mapGetters 辅助函数

```js
import { mapGetters } from 'vuex'
computed: {
    ...mapGetters(['xxx'])
}
```

