## 基础

### MVVM的理解

## 概念：

MVVM 是 Model-View-ViewModel 的缩写。

- M：Model 数据模型，也可在 Model 中定义数据修改和操作业务逻辑。
- V：view 代表UI组件，负责将数据模型转化成UI呈现出来。
- VM：ViewModel 监听数据模型的改变和控制试图行为、处理用户交互，简单理解就是一个同步 VIew 和 Model 的对象。连接 Model 和 View。





在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。



**ViewModel** 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。