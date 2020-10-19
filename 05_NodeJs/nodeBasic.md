## 创建服务器

```js
var http = require('http')

http.createServer()

server.on('request', function (request, response) {
  response.write('你好')
  response.end('something')
})

server.listen(3000, function () {
  console.log('Sever is runing at port 3000')
})
```

简写：

```js
var http = require('http')

http.createServer(function (request, response) {
  response.write('something')
  response.end('something')
})

server.listen(3000, function () {
  console.log('Sever is runing at port 3000')
})
```

