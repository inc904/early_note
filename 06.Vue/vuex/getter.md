## Getter 

### 概念：

Getter 用于 对 Store 中的数据进行加工处理形成新的数据。

 不修改 store 中的原数据，只起到包装数据的作用。

1. getter 可以对Store 中已有的数据进行加工处理之后形成新的数据，类似 Vue 中的计算属性。
2. Store 中的数据 发生变化，getter 的数据也会跟着变化。



### 使用方式：

第一种方式：

```js
this.$store.getters.xxx
```

第二种方式：

```js
import { mapGetters } from 'vuex'
computed: {
    ...mapGetters(['xxx'])
}
```

