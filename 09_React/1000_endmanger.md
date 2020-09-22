### 开始前的配置：

[参照antd配置](https://ant.design/docs/react/use-with-create-react-app-cn#高级配置)

#### 1. 引入 react-app-rewired 并修改 package.json 里的启动配置。由于新的 [react-app-rewired@2.x](https://github.com/timarney/react-app-rewired#alternatives) 版本的关系，你还需要安装 [customize-cra](https://github.com/arackaf/customize-cra)。

`react-app-rewired`（一个对 create-react-app 进行自定义配置的社区解决方案）

 `customize-cra`

```shell
yarn add react-app-rewired customize-cra -D
```

#### 然后在项目根目录创建一个 `config-overrides.js` 用于修改默认配置。

#### 2. 安装 antd

### 3. 安装sass

参照`cra`文档：[安装sass](https://www.html.cn/create-react-app/docs/adding-a-sass-stylesheet/)



使用 sass 并不需要配置。



安装less，并进行配置：

```shell 
yarn less less-loader
```

修改 `config-overrides.js` 文件。

```js
const { override,addLessLoader } = require('customize-cra')
module.exports = override(
  addLessLoader({  # 对less 的配置
    javascrpitEnabled: true
  })
)
```



### 3. [babel-plugin-import](https://github.com/ant-design/babel-plugin-import) 

是一个用于按需加载组件代码和样式的 babel 插件（[原理](https://ant.design/docs/react/getting-started-cn#按需加载)），现在我们尝试安装它并修改 `config-overrides.js` 文件。



实现按需加载

```js
const { override,fixBabelImports } = require('customize-cra')
module.exports = override(
  fixBabelImports('import', { # 实现按需加载
    libraryName: 'antd',
    libraryDirectory: 'es',
    style: true
  })
)
```

