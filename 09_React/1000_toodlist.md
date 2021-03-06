### create project folder

```shell
mkdir new_project
cd new_project
```

### npm init 初始化 项目

### npm i webpack webpack-cli

### 配置 `package.json`

```
"script": {
	"build": "webpack --config script/webpack.config.js"  # 可以配置 webpack 配置文件的地址
}
```

`npm run dev` 可以 执行 预设 的命令进行打包

### 配置 `webpack.config.js`

可以默认配置，或者可以自己配置。

```js
const path = require('path')
module.exports = {
	mode: 'development',
	entry: './src/index.js',
	output: {
		// path: path.join(__dirname, 'dist'),
		// path: path.resolve(__dirname, 'dist'),
		path: path.resolve(process.cwd(), 'dist'),
		filename: 'main.js'
	}

}
# process.cwd() ？？？
```

```js
module.exports = {
  // entry 可以配置一个对象，从而，配置多个入口文件，
  entry: {
    home: './src/home.js',
    about: './src/about.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    // filename: '[name].[chash].js'
    filename: '[name].[chunkHash:8].js'
  }
}
```

### css 预处理器

### 图片资源预处理器

### 静态资源

### babel

### cra

### 类组件

### jsx 原理

### 目录结构

#### 组件的目录结构

1.  单个组件大驼峰命名目录
2.  组件 写在 index.js 文件中
3.  私有组件 直接写在 当前调用的组件文件夹内
4.  导出： 在 components/index.js 统一处理 导出逻辑

```js
// 目录结构：
/*
components
	TodoHeader
		index.js
	TodoInput
		index.js
	TodoList
		TodoItem.js
		index.js 
*/
// 导出：
import TodoHeader from './TodoHeader'
import TodoInput from './TodoInput'
import TodoList from './TodoList'

// export {
// 	TodoHeader,
// 	TodoInput,
// 	TodoList
// }

// or
export { default as TodoHeader } from './TodoHeader'
export { default as TodoInput } from './TodoInput'
export { default as TodoList } from './TodoList'
```

### Fragment 空白组件

### props: 组件的数据挂载

#### 父组件给子组件传值

```jsx
// 父组件
render(){
	return (
        // 使用子组件的时候，传值
		<TodoHeader desc="something" x={1}>
			待办事项
		</TodoHeader>
	)
}

// 子组件
通过 props 可以拿到 props： {desc:'somrthing', children: '待办事项'}
// 在子组件中渲染
render(){
    return (
    	<div>
        	<h1>{this.props.children}</h1>
            <h2>{this.props.desc}</h2>
        </div>
    )
}
```

### prop-types 进行类型校验

执行安装命令：`npm i prop-type`

```js
import ReactTypes from 'prop-type'

// 无状态组件中校验
TodoHeader.ReactTypes = {
	desc: ReactTypes.string,
	x: ReactTypes.number.isRequired
}
TodoHeader.defaulTypes = {
	count： ReactTypes.number // 为props 设置 类型校验
}

// 有状态组件的校验
static defaultProps = {
	count: 0 // 为 props 设置默认值
}
static defaulTypes = {
	count： ReactTypes.number // 为props 设置 类型校验
}
```

### 组件的内部数据 state

this.state.someData 读取 data

this.setState({}) 设置 data

#### setState 是异步的

```js
this.setState(
  prevState => {
    return {
      isLiked: !prevState.isLiked
    }
  },
  () => {
    // 这里获取到的 才是最新的
    console.log(this.state.isLiked)
  }
)
```

### 渲染富文本内容 dangerouslySetInnerHTML,接收一个 `__html` 对象

```js
function MyComponent() {
  return <div dangerouslySetInnerHTML={{ __html: this.state.article }} />
}
```

### 事件

#### onChange 事件处理表单输入

```js
constructor(){
  this.state = {
    inputValue: 'something else'
  }
}
handleInputChange= (e) => {
  this.setState({
    inputValue: e.currentTarget.value
  })
}
render(){
  return (
    <div>
      <input
      type="text"
      value={this.state.inputValue}
      onChange={this.handleInputChange}
      />
    </div>
  )
}
```



### ref及键盘事件

### 生命周期

### 使用Ajax

- 安装axios

  `npm i axios -S`



### React-Hooks 

需要先引入

```js
import React, {useState, useEffect} from 'react'

// userState 是一个方法，方法的参数就是默认值；返回的结果是一个数组，数组的第个值就是 state, 第二个 相当于 setState
// 解构出来
const {count, setCount} = useState(0)
`<span>{count}</span>`
`<button onClick={()=>{ setCount(count + 1) }}></button>`
// count => 0
// setCount => func,

useEffect(()=>{
    // 组件的每次渲染，都会触发 useEffect，类似于 componentDidMount和componentDidUpdate
})
```

### context

### HOC

#### 基础

#### @装饰器模式

1. 装包：`react-app-rewired`

2. 安装之后，在`package.json`中将`scripts`里的`react-scripts`替换成`react-app-rewired`

3.  在根目录中创建文件`config.oberrides.js`

   ```js
   mudule.exports = (config) => {
       // 在这里去配置
       reurn config
   }
   ```

4. 配置更方便，安装`customize-cra`，然后`config-overrides.js`文件修改

   ```js
   const {override, addDecoratorsLegacy} = require('customize-cra')
   module.exports = override(
   	addDecoratorsLegacy()
   )
   ```

   



### 状态管理

#### Flux 

#### Redux

### 路由 React Router

#### 安装

```js
npm i react-router-dom -S
```

#### 组件

`BrowserRouter` `HashRouter`

`Route` `Link` `Redirect`

#### 路由API

```js
// params 传递 /artical/:id
<Link to="/artical/2">首页</Link>
// query 解析
 <Link to="/artical/2?from=artical">首页</Link>
// 使用 state 隐式传参
 <Link to={{
           pathname: '/artical/2',
           state: { // 可以在 history 的 location 中拿到
           from: 'artical'
          }
          }}>首页</Link>


<Route component={Home} path="/home" />
// 也可以用 render 函数进行渲染
<Route render={(props) => {
    // props 可以拿到 history 等参数，便于往下传递
  return  <Home x={1} ...props />
}} path="/home" />

```

### 编程式导航

```js
this.props.history.push('/home')
this.props.history.push({
    pathname: '/home',
    state: {
        id: this,props.match.parasm.id
    }
})
```

### 高阶组件

`withRouter`

### Mbox





## 扩展

### Immutable.js

### 埋点：

发送数据： 

 1. Ajax

 2. img 图片带参数

    ```js
    const img = new Image()
    img.src="http://ssdsdd.c/1.png?x=1&y=2" // 兼容性
    ```

	3. sendBeacon

    