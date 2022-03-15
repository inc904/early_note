## vuecli2 和 vuecli3

[csdn vuecli2 和 vuecli3 区别](https://blog.csdn.net/weixin_42080056/article/details/81631661)

2.0 和 3.0 项目结构

![img](https://img-blog.csdn.net/2018081316531258?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjA4MDA1Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2.0 项目安装 `vue init webpack 2.0peojectName`

3.0 项目安装 `vue create 3.0projectName`

2.0 项目启动 `npm run dev`

3.0 项目启动 `npm run serve`

## vuecli3 安装

### 全局安装：

```shell
npm install -g @vue/cli
```

安装了3.0版本还想使用2.0版本创建项目 无需卸载3.0版本。直接安装

`npm i -g @vue/cli-init `

就可以创建cli2的项目了。

[Vue2构建项目实战](https://www.cnblogs.com/zhaowy/p/8513070.html)

[Vue2项目的建立和目录的简单介绍](https://www.cnblogs.com/future-dream/p/11868566.html)



### 查看版本：

```shell
vue --version
```

### 创建项目：

#### vue create 命令

```shell
vue create [options] <app-name>
```

#### or 使用图形化界面

```shell
vue ui
```

### 配置

通过 vue-cli 3.0 工具生成的项目，默认隐藏了所有 webpack 的配置。

通过 在项目根目录新建 `vue.config.js`文件 修改 webpack 的默认配置。

```js
module.exports = {
  //  baseUrl  从 Vue CLI 3.3 起已弃用，请使用publicPath
  baseUrl: process.env.NODE_ENV === 'production' ? '/online/' : '/',
  // outputDir: 在npm run build时 生成文件的目录 type:string, default:'dist'
  // outputDir: 'dist',
  // pages:{ type:Object,Default:undfind }
  devServer: {
    port: 8888, // 端口号
    host: 'localhost',
    https: false, // https:{type:Boolean}
    open: true, //配置自动启动浏览器
    // proxy: 'http://localhost:4000' // 配置跨域处理,只有一个代理
    proxy: {
      '/api': {
        target: '<url>',
        ws: true,
        changeOrigin: true,
      },
      '/foo': {
        target: '<other_url>',
      },
    }, // 配置多个代理
  },
}
```

#### cli3.0 配置



##### 别名配置

```js
// vue.config.js
const path = require('path')
function resolve(dir){
	return path.join(__dirname, dir)
}

module.export = {
	chainWebpack: config => {
		config.resolve.alias
		// 配置别名
			.set('@', resolve('src'))
	}
}
```

#### cli4.0 配置

[使用vue-cli4.0快速搭建一个项目](https://blog.csdn.net/liyunkun888/article/details/102738377?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-3)