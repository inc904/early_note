## vue 实例的生命周期

生命周期事件，生命周期函数

- 创建时期
  - beforeCreate 这个阶段挂在对象 $el 和 data 都为 undefined，还有没有被初始化
  - created  data 有了，$el 还没有编译模板，一切在内存中创建ok，要想操作data，最早在这个时候
  - beforeMounted  模板已经编译完成，但是没有挂在到页面中去
  - mounted  将编译好的模板挂在到页面上
- 运行时期
  - beforeUpdate 此时data中的数据是最新的，但是页面中的数据不是最新的
  - updated 页面中的数据也是最新的了
- 销毁时期
  - beforeDestory
  - destoryed 不在触发生命周期