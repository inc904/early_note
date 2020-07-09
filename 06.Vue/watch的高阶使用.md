## 立即执行

'watch'是在监听属性改变时才会触发，有些时候，我们希望在组件创建后'watch'能够立即执行，可能想到的方法就是在'create'生命周期中调用一次，但这样的写法不优雅，或许我们可以使用这样的方法：

```js
export default {
  data() {
    return {
      name: 'jow',
    }
  },
  watch: {
    name: {
      handler: 'sayName',
      immediate: true,
    },
  },
  methods: {
    sayName() {
      console.log(this.name)
    },
  },
}
```

## 深度监听

在监听对象时，对象北部属性被该变时无法触发'watch',我们可以为其设置深度监听。

```js
export default {
  data() {
    return {
      student: {
        name: 'Joe',
        skill: {
          run: {
            speed: 'fast',
          },
        },
      },
    }
  },
  watch: {
    student: {
      handler: 'sayName',
      deep: true,
    },
  },
  methods: {
    sayName() {
      console.log(this.student)
    },
  },
}
```

## 触发监听执行多个方法

使用数组可以设置多项，形式包括字符串、函数、对象

```js
export default {
  data: {
    name: 'Joe',
  },
  watch: {
    name: [
      'sayName1',
      function (newVal, oldVal) {
        this.sayName2()
      },

      {
        handler: 'sayName3',
        immaediate: true,
      },
    ],
  },
  methods: {
    sayName1() {
      console.log('sayName1==>', this.name)
    },
    sayName2() {
      console.log('sayName2==>', this.name)
    },
    sayName3() {
      console.log('sayName3==>', this.name)
    },
  },
}
```

> 文档：https://cn.vuejs.org/v2/api/#watch

## watch 监听多个变量

watch 本身无法监听多个变量。但我们可以将需要监听的多个变量通过计算属性返回对象，再监听这个对象来实现“监听多个变量”

```js
export default {
  data() {
    return { msg1: 'apple', msg2: 'banana' }
  },
  compouted: {
    msgObj() {
      const { msg1, msg2 } = this
      return {
        msg1,
        msg2,
      }
    },
  },
  watch: {
    msgObj: {
      handler(newVal, oldVal) {
        if (newVal.msg1 != oldVal.msg1) {
          console.log('msg1 is change')
        }

        if (newVal.msg2 != oldVal.msg2) {
          console.log('msg2 is change')
        }
      },
      deep: true,
    },
  },
}
```
