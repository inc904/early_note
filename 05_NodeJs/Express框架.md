## Express 框架使用

优点：

1. 简介的路由定义方式
2. 对获取的HTTP请求参数进行了简化处理
3. 对模板引擎支持程度高，方便渲染动态HTML页面
4. 提供了中间件机制，有效控制HTTP请求
5. 有大量的第三方中间件对功能进行扩展

### 安装

```shell
npm i express
```

### 使用

```js
// 引入 express 框架
const express = require('express')
// 创建网站服务器
const app = express()
// 监听端口
app.listen(3000)
console.log('sever is runing ')
```

### 开放静态资源

```js
app.use(express.static('./public')) //访问方式： localhos:3000/a.txt
app.use('/public/', express.static('./public')) // localhost:3000/public/a.txt
app.use('p', express.static('./public')) // localhost:3000/p/a.txt 
```

### 路由

```js
  app.get('/', function(req,res)){
    // get 请求获取 参数 req.query
    // send()
          /*
          1. sned 方法内部会检测响应内容的类型
          2. send 方法会自动设置 http 状态码
          3. send 方法会帮我们自动设置响应的内容类型和编码
          */
    res.render()
  }
  app.post('/post',function(req, res){
    // post 请求获取 参数 req.body
    // 重定向
    res.redirect('/')
  })
```

### 渲染页面

```js
/**
 * Express 为 response 响应对象 提供了一个方法： render
 * render 方法默认是不可使用的，但是如果配置了模板引擎就可以使用了
 * response.render('html模板名', { 模板数据 })
 * 第一个参数 不能写路径，默认会去 项目中 的 views 目录中查找该模板文件
 * 也就是说 Express 约定，开发人员默认把 视图文件 都放在 views 目录中
 * 修改默认 views 目录 ：
 *  app.set('views', './public/') // 这就将 public 作为默认视图文件 存储目录
 */
```

接收 post 请求的时候 需要加载中间件 body-parser
配置 body-parser

```js
// 配置 body-parser 中间件，用来解析 表单 post 请求体
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parser application/json
app.use(bodyParser.json())
```

## 中间件

中间件主要是由两部分构成，中间件方法和请求处理函数。

中间件方法由 express 提供，负责拦截请求，请求处理函数由开发人员提供，负责处理请求。

```js
app.get('请求路径’, '处理方法')  // 接收并处理 get 请求
app.post('请求路径’, '处理方法')  // 接收并处理 post 请求        
```

可以对同一个请求设置多个中间件，对同一个请求进行多次处理。