组件中访问 state

1. `this.$stote.state.xx`

2. mapState 辅助函数，将全局数据映射为当前组件的计算属性。

   ```js
   import { mapState } from 'vuex'
   
   computed: {
       ...mapState(['xx'])
   }
   ```

   