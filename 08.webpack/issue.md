## 安装之后，没有进行任何配置，0配置文件特性

- 编译文件


- 在没有指定 输入和输出文件的时候，直接运行`webpack`命令，打包文件
默认输入文件是 `./src/index.js` 输出文件默认生路径是 `./dist/main.js`

- 命令行指定入口出口文件
```shell
webpack ./src/main.js -o ./dist/bundle.js 
```

`-o` 指定输出文件路径

- 命名行配置 编译模式
```shell
webpack --mode development ./src/main.js -o ./dist/bundle.js 
```
`--mode` 设置开发模式，可以在配置文件中配置


## 配置文件

文件名： `webpack.config.js`
最基本的配置是要配置： 入口文件和出口文件。

### 单个入口文件配置：
```js
const path = require('path') // 引入路径处理模块，node支持
module.exports = {
	entry: './input.js', // 入口文件路径配置
	output: { // 输出文件配置
		path: path.resolve(__dirname, 'dist'), // 路径配置
		filename: 'output.bundle.js' // 输出文件名
	}
}
```

### 多个入口文件配置，对象形式
```js
const path = require('path') 
module.exports = {
	entry: {
		home: './home.js',
		about: './about.js',
		other: './other.js'
	}, 
	output: { 
		path: path.resolve(__dirname, 'dist'), 
		filename: '[name].bundle.js' // [name] 对应出入文件的名字，可以输出三个不同的对应名字的输出文件
	},
	mode: "development" // production development 两种模
式}
```

配置入口出口文件之后，打包的命令是：`webpack` 

## `webapck-dev-server` 自动打包编译
1. 项目中本地安装.
依赖webpack本地包，即使在全局安装过webpack，仍需要在本地安装一次`webpack`
```shell
npm i webpack webpack-dev-server -D
```


2. 因为不是全局安装，不能直接使用命令。需要在 `package.json`中`scripts`
对象中配置命令。
```json
{
	"scripts": {
		"dev": "webpack-dev-server"
	}
}
```
3. 配置之后，此命令的用法。

```shell
npm run dev
```

`webpack-dev-server`打包的js文件并没有存储到物理磁盘上，而是托管到了电脑内存中。

### webpack-dev-server的常用参数
1. 第一种方式：
修改package.json文件
```json
{
	"scripts": {
		"dev": "webpack-dev-server --open --port 3000 --contentBase src --hot"
	}
}
```

```
--open 自动打开浏览器
--port 指定端口号，设置之后3000端口可以访问
--hot 热更新
--contentBase 指定打开的页面路径
```
修改文件之后，重启server，会执行dev中定义的命令

2. 第二种方法
不修改package.json文件
```json
{
	"scripts": {
		"dev": "webpack-dev-server"
	}
}
```
而是在 wbpack.config.js 文件中添加配置项
```js
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  mode: "development",
  devServer: {
    // contentBase: path.join(__dirname, "dist"),
    // compress: true,
    port: 9000,
    open: true,
    hot: true
  }
}
```

然后添加插件：

```js
const webpack = require('webpack')
module.exports = {

	plugins: [
		new webpack.HotModuleReplacementPlugin() // 实例化一个热更新的模块对象
	]
}
```