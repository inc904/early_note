## webpack:

1. 处理 js 文件之间的相互依赖问题
2. 处理 js 的兼容问题，把高级的，浏览器的不同语法，转化成低级的，浏览器能正常识别的语法。

```js
# 在安装一个要打包到生产环境的安装包时，你应该使用 npm install --save，如果你在安装一个用于开发环境的安装包（例如，linter, 测试库等），你应该使用 npm install --save-dev。请在 npm 文档 中查找更多信息。
```

## 安装

```shell
npm i webpack -g
npm i webpack-cli -g
```

## 手动打包 mian.js

```shell
webpack .\src\main.js -o .\dist\bundle.js --mode=development
```

## 配置文件

`webpack.config.js`

- 没有配置入口出口的时候，默认入口 src/index.js； 出口 会自动生成 dist/main.js 。
- 进行配置：

```js
const path = require('path')
module.exports = {
  mode: 'development',
  entry: './index.js', // 自己写的js代码文件
  output: {
    path: path.join(__dirname, './dist'),
    filename: 'bundle.js'
  }
}
```

之后直接运行`webpack`命令进行打包。

### 配置别名

```js
module.exports = {
    mode: 'development',
    resolve: {
        extensions: ['.js', '.jsx', '.json'], // 表示这几个文件的后缀名，可以省略不写
        alias: {
            '@': path.join(__dirname, './src') // 表示： @ 项目根目录中 src 这一层路径
        }
    }
}
```



## 自动打包编译

1. 安装 `webpack-dev-server` 工具

   工具依赖`webpack`、`webapck-cli`

2. 配置

- 在`package.json`中的配置：

```json
{
"scripts": {
  "dev": "webpack-dev-server",
## "dev": "webpack-dev-server --open --port 9000 --contentBase src"
}
}
```

配置之后，可以使用命令：`npm run dev` 打包更新程序
在配置文件中的配置，也可以配置在命令后面

- 在`webpack.config.js`中的配置,都是可选配置项
  可以使用`html-webpack-plugin`插件生成预览首页

```js
module.exports = {
  //...
  devServer: {
    contentBase: path.resolve(__dirname, '../dist'), //网站的根目录为 根目录/dist，这个路径一般与output.path一致，因为html插件生成的html5页面是放在output.path这个目录下.设置完之后，展示的就是内存中生成的新的预览页面，不在直接展示src里面的 index页面（issue： 是不是启动热更新之后，才会使用dist最为展示根目录，没有配置的时候，仍然是采用上面配置的 src/index.html）
    port: 9000, //端口改为9000
    open: true, // 自动打开浏览器，每次启动服务器会自动打开默认的浏览器
    index: 'front.html', // 与HtmlWebpackPlugin中配置filename一样
    inline: true, // 默认为true, 意思是，在打包时会注入一段代码到最后的js文件中，用来监视页面的改动而自动刷新页面,当为false时，网页自动刷新的模式是iframe，也就是将模板页放在一个frame中
    hot: false,
    compress: true //压缩
  }
}
```

webpack-dev-server 打包好的 main.js 是托管到了内存中，在物理磁盘中的项目目录中看不见。

##  使用`html-webpack-plugin`插件配置预览页面

由于使用`--contentBase`指令的过程比较繁琐，需要指定启动的目录，同时还需要修改 index.html 中 script 标签的 src 属性，所以推荐大家使用`html-webpack-plugin`插件配置启动页面.

1. 运行`cnpm i html-webpack-plugin --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：

```js
// 导入处理路径的模块
var path = require('path')

## 导入自动生成HTMl文件的插件
var htmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件
  output: {
    // 配置输出选项
    path: path.resolve(__dirname, 'dist'), // 配置输出的路径
    filename: 'bundle.js' // 配置输出的文件名
  },
  plugins: [ ## htmlWebpackPlugin插件配置
    // 添加plugins节点配置插件
    # 创建一个插件的实例
    new htmlWebpackPlugin({
      template: path.resolve(__dirname, 'src/index.html'), //模板路径
      filename: 'index.html' //自动生成的HTML文件的名称
    })
  ]
}
```

3. 修改`package.json`中`script`节点中的 dev 指令如下：

```shell
"dev": "webpack-dev-server"
```

4. 将 index.html 中 script 标签注释掉，因为`html-webpack-plugin`插件会自动把 bundle.js 注入到 index.html 页面中！

## 关于热更新（待）

webpack@4- 中，

```js
const webpcak = require('webpack')  // 第一步

module.exports = {
	// ...
	devServer: {
		hot: true // 第一步
	}
	plugins: [
		new webpack.HotModuleReplacementPlugin() // 第三步，热更新模块对象
	]
}
```

在 webapck@4+ 版本中，好像不需要。

## 关于下载源

npm 源： `registry.npmjs.org`

### 修改国内源

1. 安装`nrm` 工具

```shell
npm i nrm -g
```

2. 查看可用源列表，以及当前使用的源

```shell
nrm ls
```

3. 切换源地址

```shell
nrm use npm  ## 使用 npm 国外源
nrm use taobao ## 使用淘宝源
```
