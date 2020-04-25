https://www.onlyling.com/archives/392

## 创建项目

跟着文档提示，一步一步安装。

```
## 安装 create-react-app
npm i -g create-react-app

## 进入某个工作路径
cd yourpath

## 创建项目
npm init react-app customize-demo

## 等待项目依赖安装完成，根据控制台提示，可以 npm run start 开始使用
```

在 [webpack.config.js](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/config/webpack.config.js) 配置文件里，我们可以看到最近基本的配置。这些配置不一定符合当前的需要，例如，默认使用 `CSS`、`Scss`、`Sass` 进行样式开发，实际可能使用 `Less`，那么，我们需要自己添加配置。

如果我们要手动修改配置，官方提供了一个方式 `npm run eject`，但是这个方式不可逆。[文档](https://facebook.github.io/create-react-app/docs/available-scripts#npm-run-eject)

> Note: this is a one-way operation. Once you eject, you can’t go back!

另外可以通过第三方工具进行修改，这里推荐 `react-app-rewired`。

## 使用 react-app-rewired 自定义配置

> 
> 注意
>
> react-app-rewired 1.x 配合 create-react-app 1.x
>
> react-app-rewired 2.x 配合 create-react-app 2.x
>
> 版本升级导致互不兼容，另外，react-app-rewired 2.x 应该是社区维护了。

在 react-app-rewired 1.x 的版本中，它除了提供覆盖配置的方法，还体用了一些 `helpers`，例如 rewireLess、rewirePreact 等，2.x 版本只保留了核心功能。

From README:

> Version 2.0 removes the rewire helper functions

All helper functions:

- injectBabelPlugin
- compose
- getBabelLoader
- getLoader
- babelLoaderMatcher
- loaderNameMatches

have been removed with commit [0848602](https://github.com/timarney/react-app-rewired/commit/08486022685a5429ff3224367d89ba5acd79bde9)

另外一个工具帮我们实现了这些，[customize-cra](https://github.com/arackaf/customize-cra)，这次我们将使用 `react-app-rewired` 和 `customize-cra` 一起倒腾。

```
## 安装依赖

npm install customize-cra react-app-rewired --save-dev
```

修改项目的 `package.json`

```
{
    "scripts": {
        "start": "react-app-rewired start",
        "build": "react-app-rewired build",
        "test": "react-app-rewired test --env=jsdom"
    }
}
```

> 原来用 [react-scripts](https://github.com/facebook/create-react-app/tree/master/packages/react-scripts) 命令启动项目，现在改成 react-app-rewired 命令。

接着在项目根目录新建文件，命名为 `config-overrides.js`，也不一定要在根目录，如果要规范化开发，可以在 `package.json` 指定某个路径下的文件。

> “config-overrides-path”: “node_modules/some-preconfigured-rewire”

纯 `react-app-rewired` 的方式自定义配置，参考 [Extended Configuration Options](https://github.com/timarney/react-app-rewired#extended-configuration-options) 文档。

这次我们使用 `customize-cra` 协助自定义，参考 [Using the plugins](https://github.com/arackaf/customize-cra#using-the-plugins) 文档。

```
// 基本格式
const { override } = require('customize-cra');

module.exports = override();
```

### 使用 Less

```
## 安装依赖
npm i --save less less-loader
```

修改配置文件

```
const { override, addLessLoader } = require('customize-cra');

module.exports = override(addLessLoader());
```

`.less` 文件以及能被 less-loader 解析，并且 `.module.less` 文件将会使用 CSS Modules。自定义 CSS Modules 的 localIdentName 配置，修改 `addLessLoader({ localIdentName: '[local]--[hash:base64:5]' })` 即可。

### antd

假设我们要使用 antd，参考 [高级配置](https://ant.design/docs/react/use-with-create-react-app-cn#高级配置) 文档。

```
npm i --save-dev babel-plugin-import
npm i --save antd
const { override, fixBabelImports, addLessLoader } = require('customize-cra');

module.exports = override(
    fixBabelImports('import', {
        libraryName: 'antd',
        libraryDirectory: 'es',
        style: true,
    }), 
    addLessLoader({
        javascriptEnabled: true,
        modifyVars: { '@primary-color': '#1DA57A' },
        localIdentName: '[local]--[hash:base64:5]' // 自定义 CSS Modules 的 localIdentName
    }),
);
```

### decorators

在 create-react-app 的 [Can I Use Decorators](https://facebook.github.io/create-react-app/docs/can-i-use-decorators) 文档中说，当前它并不是一个文档的规范，默认不推荐使用，如果要使用，需要自己手动开启。

```
npm i --save-dev @babel/plugin-proposal-decorators
const { override, fixBabelImports, addLessLoader, addDecoratorsLegacy } = require('customize-cra');

module.exports = override(
    addDecoratorsLegacy(),
    fixBabelImports('import', {
        libraryName: 'antd',
        libraryDirectory: 'es',
        style: true,
    }), 
    addLessLoader({
        javascriptEnabled: true,
        modifyVars: { '@primary-color': '#1DA57A' },
        localIdentName: '[local]--[hash:base64:5]' // 自定义 CSS Modules 的 localIdentName
    }),
);
```

### 添加别名

```
const { override, fixBabelImports, addLessLoader, addDecoratorsLegacy, addWebpackAlias } = require('customize-cra');

module.exports = override(
    addDecoratorsLegacy(),
    addWebpackAlias({
        ["ag-grid-react$"]: path.resolve(__dirname, "src/shared/agGridWrapper.js")
    }),
    fixBabelImports('import', {
        libraryName: 'antd',
        libraryDirectory: 'es',
        style: true,
    }), 
    addLessLoader({
        javascriptEnabled: true,
        modifyVars: { '@primary-color': '#1DA57A' },
        localIdentName: '[local]--[hash:base64:5]' // 自定义 CSS Modules 的 localIdentName
    }),
);
```

一些简单的配置已经好了。

转载请注明：[OnlyLing - Web 前端开发者](https://www.onlyling.com/) » [create-react-app 2.x 自定义配置](https://www.onlyling.com/archives/392)

## plan 2

https://www.jianshu.com/p/7097348cd900

> 使用`create-react-app2.0`搭配`antd-mobile`构建项目后，发现官网的定制主题流程有些不符，经过一系列的探索后，决定记录下，2.0定制主题的方法。

使用`create-react-app`脚手架构建项目的过程就不说了，详情参考[创建React应用](https://links.jianshu.com/go?to=https%3A%2F%2Fcreate-react-app.dev%2Fdocs%2Fgetting-started)。
 *（注意：如果您以前`create-react-app`通过进行了全局安装`npm install -g create-react-app`，建议您使用卸载软件包，`npm uninstall -g create-react-app`以确保npx始终使用最新版本。）*

导入`antd-mobile`，参照[Ant Design Mobile of React](https://links.jianshu.com/go?to=https%3A%2F%2Fmobile.ant.design%2Fdocs%2Freact%2Fintroduce-cn)，这里不展开。

以下从成功创建`create-react-app@2.x`App及导入`antd-mobile`后开始。

### 开始

首先，你的项目里需要包含如下依赖 `babel-plugin-import less less-loader style-loader css-loader` 。



```swift
npm install --save-dev babel-plugin-import less less-loader style-loader css-loader

安装完后的依赖版本：
  "devDependencies": {
    "babel-plugin-import": "^1.13.0",
    "css-loader": "^3.2.1",
    "less": "^3.10.3",
    "less-loader": "^5.0.0",
    "style-loader": "^1.0.1"
  }
```

在不暴露`webpack`配置文件的情况下，需要使用`customize-cra`对`webpack`配置进行覆盖，再添加`react-app-rewired customize-cra`两项依赖：



```bash
npm install react-app-rewired customize-cra --save-dev

"customize-cra": "^0.9.1",
"react-app-rewired": "^2.1.5",
```

修改`package.json`文件，使用`react-app-rewired`启动、编译项目：



```cpp
/* package.json */
"scripts": {
   "start": "react-app-rewired start",
   "build": "react-app-rewired build",
   "test": "react-app-rewired test",
}
```

然后在项目根目录创建一个 `config-overrides.js` 用于修改默认配置：



```jsx
module.exports = function override(config, env) {
  // do stuff with the webpack config...
  return config;
};
```

##### ① antd-mobile按需加载

从这一步开始，官网步骤已经开始出现繁琐及错误，在不暴露`webpack`配置的情况下，是无法完成的，而一旦执行`eject`则不可逆。所以这里使用`customize-cra`对`webpack`配置进行覆盖，避免将`webpack`直接暴露出来。

修改 `config-overrides.js` 文件：



```csharp
 const { override, fixBabelImports } = require('customize-cra');

 module.exports = override(
   fixBabelImports('import', {
     libraryName: 'antd-mobile',
     libraryDirectory: 'es',
     style: 'css',
   }),
 );
```

修改`antd-mobile`组件导入方式：



```jsx
import { Button } from 'antd-mobile';
```

之后`npm start`重新启动项目，就可以看到组件样式已经是有了的。

##### ② antd-mobile定制主题

定制主题，也是在`config-overrides.js`文件进行更改



```csharp
const { override, fixBabelImports, addLessLoader } = require('customize-cra');

module.exports = override(
    addLessLoader({
      javascriptEnabled: true,
      modifyVars: {'@brand-primary': '#1DA57A'},
    }),
    fixBabelImports('import', {
      libraryName: 'antd-mobile',
      libraryDirectory: 'es',
      style: true,
    }),
);
```

使用`addLessLoader`插入`less-loader`，修改`style`为`true`，确保加载`less`文件。
 根据`modifyVars`项自由定制主题，一般由外部导入主题包赋值给`modifyVars`，这里写例子就直接写死了。关于`antd-mobile`所有可修改样式参考如下链接[全部主题样式参考这里](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fant-design%2Fant-design-mobile%2Fblob%2Fmaster%2Fcomponents%2Fstyle%2Fthemes%2Fdefault.less)。

再将样式封装一下，在项目根目录创建一个`json`文件`antd-theme.json`:



```json
{
    "@brand-primary": "#ff5722",
    "@brand-primary-tap": "#ffccbc",
    "@color-text-base-inverse": "#3f51b5"
}
```

用来存在定制的主题样式，这里修改了`primary`颜色跟字体颜色，然后在`config-overrides.js`中引入：



```jsx
const theme = require('./antd-theme');
//...
modifyVars: theme,
//...
```

修改`modifyVars`为`theme`，再修改下`App.js`做一个简单的展示：



```jsx
import React from 'react';
import { Button } from 'antd-mobile';

const App = () => {

    return (
        <div>
            <Button type="primary">antd-mobile定制主题</Button>
        </div>
    );
};

export default App;
```

最后运行`npm start`重新启动项目，就能看到效果了。



作者：讨厌西红柿
链接：https://www.jianshu.com/p/7097348cd900
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。