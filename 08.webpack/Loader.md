# 常用插件配置：

### 样式相关插件：

1. 安装

```shell
npm i style-loader css-loader -D
```

2. 在 webpack.config.js 配置。新增 module 对象，在其 rules 属性上，定义第三方模块的的匹配和处理原则。

### 处理 css
```js
moduel.exports = {
	// ...
	module: { // 配置所有第三方加载器
	rules: [
		{test: /\.css$/, use:['style-loader', 'css-loader']} // 调用规则，从右往左依次调用
	]
}
}
```
处理css，如需单独打包css文件：<https://zhuanlan.zhihu.com/p/44397561>

### 处理 less 加载器： less-loader、less 

安装：

```shell
npm install --save-dev less-loader less
```

The less-loader requires [less](https://github.com/less/less.js) as [`peerDependency`](https://docs.npmjs.com/files/package.json#peerdependencies).

```js
rules: [
		{test: /\.less$/, use:['style-loader', 'css-loader','less-loader']} 
]
```

### scss 加载器 ：sass-loader、node-sass

安装依赖：

```shell
npm install sass-loader node-sass webpack --save-dev
```

[node-sass](https://github.com/sass/node-sass) 和 [webpack](https://github.com/webpack) 是 sass-loader 的 [`peerDependency`](https://docs.npmjs.com/files/package.json#peerdependencies).

```js
rules: [
		{test: /\.scss$/, use:['style-loader', 'css-loader','sass-loader']} 
]
```

### 配置 postCSS 处理浏览器兼容性前缀

- 安装

```shell
npm install postcss-loader autoprefixer -D
```

- 配置

  在项目根目录中创建postcss的配置文件postcss.config.js,并初始化配置

  ```js
  const autoprefixer = require('autoprefixer')
  
  module.exports = {
      plugins: [ autoprefixer ] // 挂在插件
  }
  ```

- 在webpack.config.js 中配置

```js
rules: [ // 修改原来的 css loader 规则
		{test: /\.css$/, use:['style-loader', 'css-loader','postcss-loader']} 
]
```



## url-loader 处理页面资源

```shell
npm i url-lader file-loader -D
```

file-loader 是 url-loader 的依赖项。最新配置看官网

### 处理图片
```js
rules: [
		{test: /\.(jpg|png|gif|bmp|jpeg)$/, use:'url-loader'} 
]
```

后面可以添加配置，详情见官网。

### 处理字体图标
```js
rules: [
		{test: /.(ttf|woff2|gif|bmp|jpeg)$/, use:'url-loader'} 
]
```



## 处理 ES6+ 高级js语法 

babel 处理 高级语法，最新详情 见 官网。

1. 安装
 ```shell
 # 转换工具包
 npm i babel-core babel-loader@7 babel-plugin-transform-runtime  -D
 # 语法包
 npm i babel-preset-env babel-preset-stage-0 -D
 ```
 2. webpack.config.js 配置
 ```js
rules: [
  { test: /\.js$/, use: 'babel-loader', exclude: /node_modules/}
]
 ```
 3. .babelrc 配置 或者 babel.config.js，两种方式都可以

    .babelrc文件

 ```json
{
	"presets": ["env", "stage-0"],
	"plugins": ["transform-runtime"]
}		
 ```

​	.babel.config.js

```js
module.exports = {
    "presets": ["env", "stage-0"],
	"plugins": ["transform-runtime"]
}
```

最新详细配置见官网。

### 移除 webpack 严格模式

`babel-plugin-transform-remove-strict-mode`

- .babelrc 配置
```json
{
	"plugins": ["transform-remove-strivt-mode"]
}

```



