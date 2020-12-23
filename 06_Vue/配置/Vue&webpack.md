## 基本使用
### 安装

`npm i vue -D `

### 配置

安装完成后，通过`import Vue form 'vue'` 引用报错：
`You are using the runtime-only build of Vue`

需要修改 vue 文件的指向，三种方法：

1. 在 node_modules/vue/package.json 文件中的 ‘main’ 属性下，修改 vue 的文件指向
2. 在 入口js 文件中 import 其他vueJS文件的正确的路径
3. 在 webpack.config.js 文件中添加配置。
	```js
	resolve: {
    alias: {
      "vue$": 'vue/dist/vue.js'
    }
	}
	```

### .vue 格式的文件处理
#### 1. 加载器安装

```shel
npm install -D vue-loader vue-template-compiler
```
#### 2. wbepack.config.js 文件配置件配置

```js
const VueLoaderPlugin = require('vue-loader/lib/plugin')
```

```js
// 插件配置
plugins: [
	new vueloaderPlugin()
]

// 规则添加
rules: {
	{ test:/.vue$/, use: 'vue-loader' }
}
```



### 在vue组件页面中集成vue-router 路由模块

```shell
npm i vue-router
```

入口文件配置

```js
import VueRouter from 'vue-router' // 导入路由模块
Vue.use(VueRouter) //安装路由模块
var router = new VueRouter({  // 创建路由对象
	routes: [
		// code
	]
}) 
const vm = new Vue({
    el: '#app',
    render(c) { return c(App)}, // 把指定组件渲染到 el 区域
    router // 挂在到Vue
    
```

改造 App.vue 组件

```html
<template>
  <div>
  <h2>这是用户组件</h2>
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>
    <router-view></router-view>
  </div>
</template>
```

### 打包发布

pack.json 文件中配置打包命令

```json
"script": {
    "dev": "webpack",
    "bulid": "webpack -p" // 用于打包的命令
}
```

```shell
npm run bulid
```

在`/dist`中生成完整可上线项目代码

### 小知识点