## Mutation

mutation 用于变更 Store 中的数据。

1. 只能同过 mutation 变更 Store 数据，不可以直接操作 Store 中的数据。
2. 通过这种方式虽然繁琐，但是可以集中监控所有数据的变化。
3. mutation 必须同步执行

mutation 对象中的函数会有一个 state 预置参数。

```js
//  store/index.js
const ADD = 'add'
const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        add(state,paylaod){
            // 变更数据
            state.count+=paylaod.amount
        },
        [ADD](state){
          state.count+=paylaod.amount
        }
    }
})
```

### 触发 mutation 第一种方式

```js

// 组件中
 methods: {
    handleBtn(amount) {
      this.$store.commit('add', { amount })
    }
  },
  // or
 methods: {
    clickHandler(n) {
      this.$store.commit({
        type: 'subtract',
        n
      })
    }
  },
```

### 触发 mutation 第二种方式：mapMutation 辅助函数

```js
 methods: {
     // 将指定的 mutation 函数，映射为当前组件的 method
   ...mapMutations(['subtract']),
  },
```

