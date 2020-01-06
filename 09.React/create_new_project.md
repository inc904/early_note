- create project folder

```shell
mkdir new_project
cd new_project

```

- npm init 初始化 项目

- npm i webpack webpack-cli

- 配置`package.json`

```
"script": {
	"build": "webpack --config script/webpack.config.js"  # 可以配置 webpack 配置文件的地址
}
```

`npm run dev` 可以 执行 预设 的命令进行打包

- 配置`webpack.config.js`

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
- css 预处理器
- 图片资源预处理器
- 静态资源
- babel
- cra
- 类组件
- jsx原理

- 目录结构
	- 组件的目录结构
	1. 单个组件大驼峰命名目录
	2. 组件 写在 index.js 文件中
	3. 私有组件 直接写在 当前调用的组件文件夹内
	4. 导出： 在 components/index.js  统一处理 导出逻辑

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
export {default as TodoHeader} from './TodoHeader'
export {default as TodoInput} from './TodoInput'
export {default as TodoList} from './TodoList'



```

- fragment 空白组件

- props: 组件的数据挂载
父组件给子组件传值
```jsx
// 父组件
render(){
	return (
		<TodoHeader desc="something" x={1}>
			待办事项
		</TodoHeader>
	)
}

// 子组件
通过 props 可以拿到 props： {desc:'somrthing', children: '待办事项'}
```
- prop-types 进行类型校验

```shell
npm i prop-type
```


```js
import ReactTypes from 'prop-type'

// 无状态组件中校验
TodoHeader.ReactTypes = {
	desc: ReactTypes.string,
	x: ReactTypes.number.isRequired
}


// 有状态组件的校验
static defaultProps = {
	count: 0 // 为 props 设置默认值
}
static defaulTypes = {
	count： ReactTypes.number // 为props 设置 类型校验
}
```

- 组件的内部数据 state
