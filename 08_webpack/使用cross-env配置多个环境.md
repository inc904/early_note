## cross-env

**cross-env**这是一款运行跨平台设置和使用环境变量的脚本

cross-env 的作用是不需要全局配置 NODE_ENV 在 scripts 脚本中修改 NODE_ENV 的值从而实现不同环境中 proccess.env.NODE_ENV 的不同，而 config 的工作原理就是基于 NODE_ENV 这个值的，所以推荐两者结合使用。

### 安装

`npm install --save-dev cross-env`

NODE_ENV=production

`npm run dev` 打包的是开发环境
`npm run build--qa` 打包的是测试环境
`npm run build--prod` 打包的是生成环境

```json
{
  "dev": "cross-env NODE-ENV=development node build/webpack.deb.conf.js",
  "build --qa": "cross-env NODE_ENV=testing node build/build.js",
  "build --prod": "cross-env NODE_ENV=production node build/build.js"
}
```

```js
//dev环境 build/wbpack.dev.config.js
module.exports = {
  NODE_ENV: '"development"',
  BASE_API: "http://10.250.115.99/statistics", //代理路径
};
//测试环境  build/wbpack.test.config.js
module.exports = {
  NODE_ENV: '"testing"',
  BASE_API: "http://10.250.115.99/statistics", //代理路径
};
//生产环境  build/wbpack.prod.config.js
module.exports = {
  NODE_ENV: '"production"',
  BASE_API: "http://ai.iteldrive.com/statistics", //代理路径
};
```

#### 修改 config/index.js (注意新增 prodEnv、testEnv)

```js
"use strict";
const path = require("path");

module.exports = {
  build: {
    prodEnv: require("./prod.env"),
    testEnv: require("./test.env"),
    index: path.resolve(__dirname, "../dist/index.html"),
    assetsRoot: path.resolve(__dirname, "../dist"),
    assetsSubDirectory: "static",
    assetsPublicPath: "./",
    productionSourceMap: true,
    devtool: "#source-map",
    productionGzip: false,
    productionGzipExtensions: ["js", "css"],
    bundleAnalyzerReport: process.env.npm_config_report,
  },
};
```

#### 在 webpackage.prod.conf.js 中配置构建环境参数

```js
const env =
  process.env.NODE_ENV === "testing"
    ? require("../config/test.env")
    : require("../config/prod.env");
```

#### 调整 build/build.js

```js
var spinner = ora(``'building for '` `+ process.env.NODE_ENV + '...')
spinner.start()
```

以上步骤配置完毕之后，重启 npm run build--qa，此时就会发现运行测试环境的代码已经打包生成好了（dist 目录），问题是环境配好了，怎么配置不用环境的 api 呢？

#### 配置不同环境 api，根据匹配 NODE_ENV 的不同的值

```js
let API_URL;
if (process.env.NODE_ENV === "development") {
  API_URL = "http://10.250.115.99/statistics";
} else if (process.env.NODE_ENV === "production") {
  // 测试环境
  API_URL = "http://ai.iteldrive.com/statistics";
} else if (process.env.NODE_ENV === "testing") {
  API_URL = "http://10.250.115.99/statistics";
} else {
  API_URL = "http://ai.iteldrive.com/statistics";
}
//console.log(API_URL + '请求api************')
const http = axios.create({
  baseURL: API_URL, // api的base_url,
  timeout: 1000 * 30,
  withCredentials: true,
  headers: {
    "Content-Type": "application/json; charset=utf-8",
  },
});
```

现在分别执行 npm run dev、npm run build --qa 和 npm run build --prod 就可以得到想要的结果了
