## React 和 Vue 的对比

### 组件化方面：

#### 什么是模块化：

从`代码`的角度进行分析的。把一些可复用的代码，抽离为单个的模块；便于项目的开发和维护。

#### 什么是组件化：

从`UI界面`的角度来进行分析；把一些可复用的 UI 元素抽离为单独的组件；便于项目的开发和维护；

#### 组件化的好处：

随着项目的增大，手里的组件越来越多；很方便把现有的组件，拼接出以恶搞完整的页面

#### Vue 是如何实现组件化的：

`.vue`文件

- template 结构
- script 行为
- style 样式

#### React 是如何实现组件化的：

一切都是以 js 来表现的。

## React 核心思想

### 核心

- 组件化

- 虚拟 DOM

- JSX

  虚拟 DOM 写起来比较麻烦，所有提供了 'JSX '的方式

### DOM 和 虚拟 DOM

- **DOM 的本质**：

  浏览器中的概念，用 js 对象来表示页面上的元素，并提供了操作 DOM 对象的 API；

- React 中的虚拟 DOM：

  框架中的概念，用 js 对象来模拟页面上的 DOM 和 DOM 嵌套

- 为什么要实现虚拟 DOM

  为了实现页面中 DOM 元素的高效更新

### Diff 算法

- Tree Diff：

  新旧两棵 DOM 树，逐层对比的过程。

  - 当整棵 DOM 逐层对比完毕，则所有需要被更新的元素，必然能被找到。

- Component Diff：

  在进行 tree Diff 的时候，每一程，组件级别的对比。

  - 如果对比前后，组建的类型相同，则`暂时`认为此组件不需要被更新
  - 如果对比前后，组件的类型不同，则需要移除旧组件，创建新的组件，并追加到页面上。

- Element Diff：

  在进行组件对比的时候，如果两个组件类型相同，则需要进行 `元素` 级别的对比。

## Quick Start

### Trying out React

- 云端编程环境
  - 只是用于 demo 测试
- 脚手架工具： `create-react-app`
  - 正式开发环境
  - 类似于 `vue-cli`
  - 集成了 webpack 构建工具等环境
- 本地简单开发测试（没有模块化支持）
- 自己动手搭建模块化 webpack 开发环境

#### 初始化及安装依赖

```shell
npm i react react-dom @babel/standalone
```

- @babel/standalone
  可以在浏览器中调用 babel 的 API 完成 ES6 -> ES5 的转换

## 在项目中使用 React

1. 装包

   ```shell
   npm i react react-dom -S

   ```

   - react： 用于创建组件和虚拟 DOM，同时组件的生命周期都在这个包中。
   - react-dom：专门用于进行 DOM 操作，最主要的应用场景就是 `ReactDOM.render()`

2. 在 `index.html`中创建容器

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟 DOM 元素，都会被渲染到这个指定的人容器中。 -->
   <div id="app"></div>
   ```

3. 导入包：

   ```js
   import React from 'react'
   import ReactDOM from 'react-dom'
   ```

4. 创建虚拟 DOM 元素

## React 中创建组件

## 组件的生命周期

- 创建阶段

  - `componentWillMount`：
    - 组件将要被挂载，此时还没有渲染虚拟 DOM；
    - 此时无法获取页面元素；
    - 可以获取页面初始化的 state 和 props；
    - 可以访问自己定义的函数；
    - 等同于 `Vue` 中的，`created`钩子函数。
  - `render`：
    - 第一次开始渲染真正的虚拟 DOM，当 Render 执行完了，内存中就有了完整的虚拟 DOM；
    - 页面中没有真正显示，获取不到页面中的元素；
  - `componentDidMount`：
    - 组件完成了挂载，此时组件已经显示到了页面上，当这个方法执行完毕，组件就进入到了运行阶段；
    - 可以获得页面上的元素；想要`操作DOM元素`，最早在这里；
    - 相当于`Vue`中的 `mounted`钩子函数

- 组件运行阶段

  - `componentWillReceiveProps(nextProps)`：
    - 组件将要接收新的属性，此时，只要这个方法被触发，就证明父组件为当前子组件传递了新的属性。
  - `shouldComponentUpdate(nextProps, nextState)`：
    - 组件是否需要被更新，此时，组件尚未被更新，但是，state 和 props 肯定是最新的。
  - `componentWillUpdata(nextProps, nextState)`：
    - 组件将要被更新，此时，尚未开始更新，内存中的虚拟 DOM 还是旧的，
  - `render`：
    - 此时，又要重新根据最新的 state 和 props 重新渲染一棵内存中的虚拟 DOM 树，当 render 函数调用完毕，内存中的旧的 DOM 树，已经被新的 DOM 树替换了。此时，页面中还是旧的
  - `componentDidUpdate(prevProps, prevState)`：
    - 此时，页面又被重新渲染了，state 和 虚拟 DOM 和 页面 已经保持同步。

- 组件销毁阶段

  - `componentWillUnmount`：
  - 此时组件将要被卸载

  ​

## getChildrenContextTypes 越组件传值方式

前三 后三 后俩

## 路由
