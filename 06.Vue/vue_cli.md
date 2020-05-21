## vuecli2和vuecli3

2.0和3.0项目结构

![img](https://img-blog.csdn.net/2018081316531258?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MjA4MDA1Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2.0 项目安装 `vue init webpack 2.0peojectName`

3.0 项目安装 `vue create 3.0projectName`



2.0 项目启动 `npm run dev`

3.0 项目启动 `npm run serve`

## vuecli3安装

### 全局安装：

```shell
npm install -g @vue/cli
```

### 查看版本：

````shell
vue --version
````

### 创建项目：

#### vue-create

```shell
vue create [options] <app-name>
```



#### 使用图形化界面

````shell
vue ui
````

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
                changeOrigin: true
            },
            '/foo': {
                target: '<other_url>'
            }
        },  // 配置多个代理
    }
}
```

