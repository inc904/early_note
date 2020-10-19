
从3.0 开始，之前的build和config文件夹就取消了。

如果需要更改配置，只需要在项目的根目录下新建 vue.config.js 文件，来覆盖项目的配置。（是根目录，不是src目录）

语法

```js
module.exports = {
  // 基本路径 baseURL已经过时
  publicPath: './',  
  // 输出文件目录
  outputDir: 'dist',
  // eslint-loader 是否在保存的时候检查
  lintOnSave: true,
  // use the full build with in-browser compiler?
  // https://vuejs.org/v2/guide/installation.html#Runtime-Compiler-vs-Runtime-only
  // compiler: false,
  // webpack配置
  // see https://github.com/vuejs/vue-cli/blob/dev/docs/webpack.md
  chainWebpack: () => {},
  configureWebpack: () => {},
  // vue-loader 配置项
  // https://vue-loader.vuejs.org/en/options.html
  // vueLoader: {},
  // 生产环境是否生成 sourceMap 文件
  productionSourceMap: true,
  // css相关配置
  css: {
   // 是否使用css分离插件 ExtractTextPlugin
   extract: true,
   // 开启 CSS source maps?
   sourceMap: false,
   // css预设器配置项
   loaderOptions: {},
   // 启用 CSS modules for all css / pre-processor files.
   modules: false
 },
  // use thread-loader for babel & TS in production build
  // enabled by default if the machine has more than 1 cores
  parallel: require('os').cpus().length > 1,
  // 是否启用dll
  // See https://github.com/vuejs/vue-cli/blob/dev/docs/cli-service.md#dll-mode
  // dll: false,
  // PWA 插件相关配置
  // see https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-pwa
  pwa: {},
  // webpack-dev-server 相关配置
  devServer: {
  	open: process.platform === 'darwin',
   host: '0.0.0.0',//如果是真机测试，就使用这个IP
   port: 1234,
   https: false,
   hotOnly: false,
   proxy: null, // 设置代理
   before: app => {}
 },
  // 第三方插件配置
  pluginOptions: {
   // ...
 }
}
```

Vue.config.js配置跨域
```js
devServer: {
        open: true, //浏览器自动打开页面
        host: "0.0.0.0", //如果是真机测试，就使用这个IP
        port: 8911,
        https: false,
        hotOnly: false, //热更新（webpack已实现了，这里false即可）
        proxy: {
            //配置跨域
            '/api': {
            	target: "http://192.168.234.237:8886/api",
            	ws:true,
            	changOrigin:true,
            	pathRewrite:{
            		'^/api':'/'
            	}
            }
          }
        }

//调用
this.$http.get('/api/order/getOrder')
.then(res => {
	console.log(res.data);
})
.catch(err => {
	console.log(err.data.message);
});
```