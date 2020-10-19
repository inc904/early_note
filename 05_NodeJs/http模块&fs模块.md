### 0.模块
- 具名得核心模块
- 自定义模块
- 在 node 中没有全局作用域，只有模块作用域。
### 0.1 模块之间的通信
- 如何在模块之间进行通信
    + 默认都是封闭的
- require 方法有两个作用
    1. 加载模块并执行里面的代码
    2. 拿到被加载文件模块导出的接口对象
- 在每个文件模块中都提供了一个对象`exports`
    `exports` 默认是一个空对象
    把需要外部访问得成员挂载到`exports`对象中
    ```js
    var foo = 'hello'
    // 1.分别挂载
    exports.foo = foo
    exports.name = 'jojo'
    export.add = function(){
        console.log('qqq')
    }
    // 2.集体挂载
    exports = []
    ```
### 1.HTTP系统模块--创建服务器
http协议
```js
// 1.加载 http 核心模块
var http = require('http')
// 2.创建一个 web 服务器
var server = http.createServer()
// 3.服务器提供服务：对数据的服务
/*
    发请求
    接受请求
    处理请求
    给个反馈（发送响应）
*/
// 注册 request 请求事件
// 当服务器请求过来，就会自动触发服务器的 request 事件，她然后执行回调处理函数
server.on('request', function(){
    console.log('收到客户端的请求了')
})
// 4. 绑定端口号，启动服务器
server.listen(3000, function(){
    console.log('服务器启动成功了，通过 http://localhost:3000 访问')
})


```
### 2.fs模块-文件操作
```js
// 加载文件模块
var fs = require('fs) 

// 读取文件
fs.readFile('filePath',function(error,data){
    #code...
    // error 是错误信息
    // /data 是读取到的文件数据
})
// 写文件
fs.writeFile('filePath','fileContent',function(error){
    #code...
    // error 错误信息
})
```