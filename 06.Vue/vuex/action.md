## Aciton 处理异步任务

如果通过异步操作变更数据，必须通过 action ，不能直接 使用 mutation，但是在 action种还是要通过触发同步 mutation 的方式 间接变更数据。

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

