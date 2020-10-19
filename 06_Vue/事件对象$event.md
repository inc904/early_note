`$event ` 是事件对象的特殊变量，在一些场景给我们实现复杂功能提供更多可用的参数。

## 原生事件

在原生事件中表现和默认事件对象相同。

```html
<template>
  <div>
    <input type="text" @input="inputHandler('hello,', $event)" />
  </div>
</template>
<script>
  export default {
    methods: {
      inputHandler(msg, e) {
        console.log(e.target.value)
      },
    },
  }
</script>
```

## 自定义事件

在自定义事件中表现为捕获从子组件抛出的值

```html
<!-- MyItem.vue -->
<script>
  export default {
    methods: {
      customEvent() {
        this.$emit('custom-event', 'some value')
      },
    },
  }
</script>
```

```html
<template>
  <div>
    <my-item
      v-for="(item, index) in list"
      @custom-event="customEvent(index, $event)"
    />
  </div>
</template>
<script>
  export default {
    methods: {
      customEvent(index, e) {
        console.log(e) // 'some value'
      },
    },
  }
</script>
```

> 文档：https://cn.vuejs.org/v2/guide/events.html# 内联处理器中的方法

> https://cn.vuejs.org/v2/guide/components.html# 使用事件抛出一个值
