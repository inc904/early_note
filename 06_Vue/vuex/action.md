## 概念

-  action 提交 mutation ，不直接改变状态
- action 函数的预置参数 context，是一个与store 具有相同方法和属性的 对象，但不是 store 实例本身
- 可以 调用 context.commit 提交一个 mutation，或者通过 context.store 和 context.getters 来获取 store 和 getters

实践中，通过参数解构来简化代码
```js
action:{
    increment({commit}){
        // 调用 事件类型为 'increment'的 mutation，提交的载荷为 2
        commit('increment',2) 
    }
}

// 购物车实例，涉及调用异步api和分发多重 mutation
action:{
    checkout({c
        // 成功操作omit, state}, products){
        // 把当前购物车的物品备份起来
        const savedCartItems = [...store.cart.added]
        // 发出结账请求，然后清空购物车
        commit(types.CHECKOUT_REQUEST)
        // 购物车 api 接受 一个成功回调 一个 失败回调
        shop.buyProducts(
            products,
            // 成功操作
            () => commit(tyeps.CHECKOUT_SUCCESS),
            // 失败操作
            () => commit(types.CHECKOUT_FAILURE, savedCartItems)
            )
    }
}
```

aciton 通过 `store.dispacth` 方法触发
```js
store.dispatch('increment')

// 同事 actions 支持载荷的方式和对象的方式分发

// 载荷形式
store.dispatch('increment',{
    amount: 10
})

// 对象形式分发
store.dispatch({
    type: 'incrementAsync',
    amount: 10
})
```

## Aciton 处理异步任务

如果通过异步操作变更数据，必须通过 action ，不能直接 使用 mutation，但是在 action 中还是要通过触发同步 mutation 的方式 间接变更数据。

#### store中定义actions
```js
// store/index.js
const store = new Vuex.Store({
    state:{
        count: 0
    }
    mutation: {
   		 add (state){
        state.count++
    	}
    },
    action: {
        addAsync({commit}){
            setTimeout(()=>{
                commit('add')
            }, 1000)
        }
    }
})
```

#### 在组件中分发 actions

```js
// 组件中

import { mapState, mapMutations, mapActions } from 'vuex'
methods: {
	// 方法1. 借助 mapActions 辅助函数
    ...mapActions(['subtractAsync']),
     // 方法2. 通过dispatch
    handleBtn2(amount) {
      this.$store.dispatch('addAsync', { amount })
    }
  },
```

### 组合 actions

`store.dispath` 可以处理被触发的 aciton 的处理函数返回的 Promise，并且 `store.dispatch` 仍然返回 promise
```js
actions:{
    actionA({commit}){
        return new Promise((resolve, reject)=>{
            setTimeout(()=>{
                commit('someMutation')
                resolve()
            }, 1000)
        })
    }
}
```
```js
store.dispatch('actionA').then(()=>{})
```

```js
actions:{
    actionB({dispatch,commit}){
        return dispatch('actionA').then(()=>{
            commit('someMutation')
        })
    }
}

// async/await 写法
actions:{
    async actionA({commit}){
        commit('gotData', await getData())
    },
    async actionB({dispatch, commit}){
        await dispatch('actionA') // 等待 actionA 完成
        commit('gotOtherData', await getOtherData())
    }
}
```

一个 store.dispatch 在不同模块中可以触发多个 action 函数。在这种情况下，只有当所有触发函数完成后，返回的 Promise 才会执行。