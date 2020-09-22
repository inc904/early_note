## JSX

HTML 语言直接写在 JavaScript 语言中，不写任何引号，这就是 JSX 语法。它允许 HTML和 JavaScript 混写。

### 环境配置

- 非模块化环境
  - `babel-standalone`
  - 执行时编译，比较慢，只适用于开发测试环境
- 模块化环境
  - `babel-prese-react`
  - 结合 webpack 配置相应的工具
  - 浏览器执行的是预编译结果
- Bebal REPL赋值 查看编译结果
  - 适用于在线测试

### 基本语法

- 有且仅有一个根节点
- 多标签写在一个 小括号中
- 遇到 HTML 标签（以`<`开头）就用HTML规则解析
  - 单标签不能省略结束标签
- 遇到代码块（以`{`开头）就用 JavaScript 规则解析
- JSX 允许直接在模版中插入一个 JavaScript 变量
  - 如果这个变量是一个数组，则会展开这个数组的所有成员添加到模版中
- 单标签必须结束`/>`
  - `<img  />`、`<input />`

### 在JSX中嵌入JavaScript 表达式



### 启用JSX 语法

- 安装`babel`插件

  - ```shell
    ## 安装 babel 插件
    npm i babel-core babel-loader babel-plugin-transform-runtime -D
    
    npm i babel-preset-env babel-preset-stage-0 -D
    ## 安装能够识别转换 JSX 语法的包
    npm i babel-preset-react -D
    
    ```

npm install --save-dev @babel/preset-react

​      转换工具包

```shell
 npm i babel-core babel-loader@7 babel-plugin-transform-runtime  -D
```




​      语法包

    ```
      npm i babel-preset-env babel-preset-stage-0 -D
    ```

- 添加`.babelrc`配置文件
  
    ```json
    {
        "presets": ["env", "stage-0", "react"],
        "plugin": ["transform-runtime"]
    }
    ```
  
    

#### nice road

```shell
npm i @babel/core @babel/preset-env @babel/runtime @babel/plugin-transform-runtime @babel/plugin-proposal-class-properties @babel/preset-react -D
```



`.babelrc`配置

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"],
  "plugins": [
    "@babel/transform-runtime",
    "@babel/plugin-proposal-class-properties"
  ]
}

```

`webpack.config.js`配置

```js
module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        loader: 'babel-loader',
        exclude: /node_modules/
      }
    ]
  }
```

### jsx 语法的本质：

​	并不是直接把 jsx 渲染到页面上，而是内部先转换成了 createElement 形式，再渲染。

### 在 jsx 中混合写入 js 表达式：

​	在 jsx 语法中，要把 js 代码写在`{}`中；

- 渲染数字
- 渲染字符串
- 渲染布尔值
- 为属性绑定值
- 渲染 jsx 元素
- 渲染 jsx 元素数组
- 将普通字符转换为 jsx 数组帮渲染页面上【两种方法】

### 在 jsx 中写注释

​	推荐使用：`{/* 这是注释 */}`

