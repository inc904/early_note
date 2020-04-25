> 使用`create-react-app2.0`搭配`antd-mobile`构建项目后，发现官网的定制主题流程有些不符，经过一系列的探索后，决定记录下，2.0定制主题的方法。

使用`create-react-app`脚手架构建项目的过程就不说了，详情参考[创建React应用](https://links.jianshu.com/go?to=https%3A%2F%2Fcreate-react-app.dev%2Fdocs%2Fgetting-started)。
 *（注意：如果您以前`create-react-app`通过进行了全局安装`npm install -g create-react-app`，建议您使用卸载软件包，`npm uninstall -g create-react-app`以确保npx始终使用最新版本。）*

导入`antd-mobile`，参照[Ant Design Mobile of React](https://links.jianshu.com/go?to=https%3A%2F%2Fmobile.ant.design%2Fdocs%2Freact%2Fintroduce-cn)，这里不展开。

以下从成功创建`create-react-app@2.x`App及导入`antd-mobile`后开始。

## 开始

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

![img](https:////upload-images.jianshu.io/upload_images/1940241-5ae640ccecef094f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/468/format/webp)

1575621602936.jpg



如此，关于`antd-mobile`定制主题就成功了，也不需要暴露`webpack`配置，也没有antd-mobile官网写的那么多乱七八糟的步骤，保持项目的整洁。

## 最后

**什么？你的定制主题还是没显示？**

1. 请检查项目构建流程是否有按照以上步骤进行；
2. 请检查你的定制主题属性，是否与你显示的组件对应
    比如：你写了这一条定制样式`'@brand-primary': '#1DA57A'`，对应的是组件`primary`样式，则你的组件需要加上`type='primary'`属性才生效；
3. 请确认`style`属性已经设置成`true`;
4. 请确认各项依赖版本号，`react-app-rewired`需要`2.0.0`以上；



作者：讨厌西红柿
链接：https://www.jianshu.com/p/7097348cd900
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。