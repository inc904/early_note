## react 核心思想

### 核心

- 组件化

- 虚拟 DOM

- JSX

    虚拟 DOM 写起来比较麻烦，所有提供了 JSX 的方式

    

### DOM 和 虚拟 DOM

- **DOM的本质**：

  浏览器中的概念，用 js 对象来表示页面上的元素，并提供了操作 DOM 对象的 API；

- React 中的虚拟 DOM：

  框架中的概念，用 js 对象来模拟页面上的 DOM 和 DOM 嵌套

- 为什么要实现虚拟 DOM

   为了实现页面中 DOM 元素的高效更新

### diff算法

- Tree Diff：

  新旧两棵DOM树，逐层对比的过程。

  + 当整棵DOM逐层对比完毕，则所有需要被更新的元素，必然能被找到。

- Component diff： 

  在进行 tree Diff 的时候，每一程，组件级别的对比。

  + 如果对比前后，组建的类型相同，则`暂时`认为此组件不需要被更新
  + 如果对比前后，组件的类型不同，则需要移除旧组件，创建新的组件，并追加到页面上。

- Element Diff：

  在进行组件对比的时候，如果两个组件类型相同，则需要进行 `元素` 级别的对比。


## Quick Start
### Trying out React
- 云端编程环境
    + 只是用于 demo 测试
- 脚手架工具： `create-react-app`
    + 正式开发环境
    + 类似于 `vue-cli`
    + 集成了 webpack 构建工具等环境
- 本地简单开发测试（没有模块化支持）
- 自己动手搭建模块化 webpack 开发环境
#### 初始化及安装依赖
```shell
npm i react react-dom @babel/standalone
```
- @babel/standalone
可以在浏览器中调用 babel 的API 完成 ES6 -> ES5 的转换