### 需求

项目会有很多环境，比如最常用会有一下环境，
develop：本地开发环境
alpha：测试/预发布环境
production：正式/生产环境
不同环境下，打包、部署和 API 的调用都是不同的。
如果每次都频繁修改代码，明显是不理智的

按照命令调用不同配置文件启动呢？

### 使用

#### 1、在 package.json 新增命令脚本

```json
"scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "serve:alpha": "vue-cli-service serve --mode alphaser",
    "build:alpha": "vue-cli-service build --mode alpha"
  },
```

#### 2、在项目根目录下，新增配置文件

```js
#	env.alpha
#	env.development
# 	env.production
```

--mode alpha 意思为指定环境模式为alpha ,会调用 .env.alpha  文件。默认不指定则为development。所以我们建立多个配置文件

**.env.alpha**

```
NODE_ENV = development
BASE_URL = /
VUE_APP_ENV = development
VUE_APP_ENV_CHN = 前端环境：本地开发环境。 后端环境：测试服环境
VUE_APP_SERVER = https://t-12368-h5.aegis-info.com/casservice/web/v1/
```

**.env.production**

```
NODE_ENV = production
BASE_URL = /caspage/
VUE_APP_ENV = production
VUE_APP_ENV_CHN = 前端环境：正式环境。 后端环境：正式服环境
VUE_APP_SERVER = https://shandong-12368.aegis-info.com/casservice
```

#### 然后对vue项目改造

### **vue.config.js **文件

- 动态配置打包的路径和目录（即项目内所有的请求链接地址都是publicPath）
- 本地开发代理地址proxy

```js
module.exports = {
  publicPath: process.env.BASE_URL,
  devServer: {
    proxy: process.env.VUE_APP_SERVER
  }
};
```

### Axios 配置

```js
// 本地会自动走vue.config.js里的代理地址，不需要配置baseUrl。否则代理会失效
if (process.env.VUE_APP_ENV !== 'development') {
  axios.defaults.baseURL = process.env.VUE_APP_SERVER;
}


```

### history模式 配置

配置路由，因为服务器可能不一定将你的项目放在根目录下

```
const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})
```

## vue-cli 3.0版本配置环境

### 1、新建 vue.config.js 文件

### 2、新建 config 文件夹，存放 环境配置文件：pro.env.js（生产环境配置），uat.env.js（测试环境配置）, dev.env.js（本地环境）

文件内容：

```js
// 生产环境
module.exports = {
    NODE_ENV: '"production"',
    hosturl:''
}
```

```js
// 测试环境
module.exports = {
    NODE_ENV: '"test"',
    hosturl:''
}
```

```js
const hosturl= '';
// 本地环境
module.exports = {
    NODE_ENV: '"development"',
    hosturl:hosturl
}
```

### 3、vue.config.js 内容配置

```js
var path = require('path');

const devProxy = ['/pc','/weixin','android',...];  // 代理
var proEnv = require('./config/pro.env');  // 生产环境
var uatEnv = require('./config/uat.env');  // 测试环境
var devEnv = require('./config/dev.env');  // 本地环境
const env = process.env.NODE_ENV;
let target = '';

# 对项目环境的 判断

// 默认是本地环境
if(env==='production'){  // 生产环境
    target = proEnv.hosturl;
}else if(env==='test'){ // 测试环境
    target = uatEnv.hosturl;
}else{  // 本地环境
    target = devEnv.hosturl;
}
# 生成代理配置对象
let proxyObj = {};
devProxy.forEach((value, index) => {
    proxyObj[value] = {
        target: target,
        changeOrigin: true,
        pathRewrite: {
            [`^${value}`]: value
        }
    };
});

module.exports = {
    baseUrl: '/',
    outputDir: 'dist',
    devServer: {
        // open: process.platform === 'darwin',
        host: '0.0.0.0',
        port: 8080,
        https: false,
        hotOnly: false,
        disableHostCheck: true, # 配置反向代理
        // See https://github.com/vuejs/vue-cli/blob/dev/docs/cli-service.md#configuring-proxy
        proxy: proxyObj, // string | Object
        before: app => {}
    }
};
```

### 4、package.json 文件配置

```json
"scripts": {
    "dev": "vue-cli-service serve --open",
    "prod":"vue-cli-service build --mode=production",
    "uat": "vue-cli-service build --mode=test" 
  },
```

#### serve 和build 的区别

serve 是服务命令，build是用于打包用的，比如 npm run dev ,可以在浏览器上直接浏览页面，prod和uat 这两个就只能在本地打好包，然后放到服务器上，访问网址才能看到。

代理 不同环境 走不同的target就配置好了。

### 5、注意

#### cli-service 服务命令，默认情况下必须有一个development

```
--open    open browser on server start
  --mode    specify env mode (default: development)
  --host    specify host (default: 0.0.0.0)
  --port    specify port (default: 8080)
  --https   use https (default: false)
```

#### 模式

**模式**是 Vue CLI 项目中的一个重要概念。默认情况下，Vue CLI项目中有**三种**模式：

- **development**  用于 vue-cli-service serve

- **production** 被vue-cli-service build和使用vue-cli-service test:e2e

- **test** 用于 vue-cli-service test:unit

请注意，模式不同NODE_ENV，因为模式可以包含多个环境变量。也就是说，NODE_ENV默认情况下每个模式都设置为相同的值 - 例如，NODE_ENV将设置为"development"开发模式。

您可以通过后缀.env文件来设置仅适用于特定模式的环境变量。例如，如果创建.env.development在项目根目录中命名的文件，则在该文件中声明的变量将仅在开发模式下加载。

您可以通过传递--mode选项标志来覆盖用于命令的默认模式。例如，如果要在build命令中使用开发变量，请将其添加到package.json脚本中：

"dev-build": "vue-cli-service build --mode development",
示例：分段模式

假设我们有一个包含以下.env文件的应用：

```
VUE_APP_TITLE=My App
```

以下.env.staging文件：

```
NODE_ENV=production
VUE_APP_TITLE=My App (staging)
```

vue-cli-service build建立一个生产应用程序，装载 .env，.env.production以及.env.production.local如果它们存在;

vue-cli-service build --mode staging建立在分段模式中，使用生产应用.env，.env.staging以及.env.staging.local如果它们存在。

在这两种情况下，应用程序都是作为生产应用程序构建的，因为NODE_ENV它在暂存版本中process.env.VUE_APP_TITLE会被不同的值覆盖。



## 参考文档：

[vue不同环境下的配置](https://www.cnblogs.com/dshvv/p/12889464.html)

[vue-cli 3.0版本，配置代理Proxy，不同环境不同target（生产环境，uat环境和本地环境的配置）](https://www.cnblogs.com/zuoan-oopp/p/9101240.html)

[vue相关配置文件详解及多环境配置详细步骤](https://www.jb51.net/article/186839.htm)

[vue config.js配置生产环境和发布环境不同的接口地址问题](https://www.cnblogs.com/maqingyuan/p/9036803.html)

[vue多环境配置方案](https://segmentfault.com/a/1190000019136606)

[vue-cli2多环境配置](https://www.jianshu.com/p/c35086d299b8)