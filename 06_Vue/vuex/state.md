组件中访问 state

1. `this.$stote.state.xx`

2. mapState 辅助函数，将全局数据映射为当前组件的计算属性。

   ```js
   import { mapState } from 'vuex'
   
   computed: {
       ...mapState(['xx'])
   }
   ```


 使用 Vuex 并不意味着你需要将所有的状态放入 Vuex。

 如果有些状态严格属于单个组件，最好还是作为组件的局部状态。