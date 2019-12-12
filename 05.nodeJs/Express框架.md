## Express框架
- 开放静态资源
```js
  app.use(express.static('./public')) //访问方式： localhos:3000/a.txt
  app.use('/public/', express.static('./public')) // localhost:3000/public/a.txt
  app.use('p', express.static('./public')) // localhost:3000/p/a.txt
```
- 路由
```js
  app.get('/', function(req,res)){
    // get 请求获取 参数 req.query
    res.render()
  }
  app.post('/post',function(req, res){
    // post 请求获取 参数 req.body
    // 重定向
    res.redirect('/')
  })
```
- 渲染页面
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
- 接收 post 请求的时候 需要加载中间件 body-parser
  配置 body-parser
  ```js
    // 配置 body-parser 中间件，用来解析 表单 post 请求体
    // parse application/x-www-form-urlencoded
    app.use(bodyParser.urlencoded({ extended: false }))
    // parser application/json
    app.use(bodyParser.json())
  ```