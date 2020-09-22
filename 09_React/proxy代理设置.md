

如果proxy的值是字符串，不需要修改

如果proxy的值是一个json，则需要做如下修改:

1. npm install http-proxy-middleware

    [http-proxy-middleware](https://www.npmjs.com/package/http-proxy-middleware)

2. src文件夹根目录下创建 setupProxy.js 文件

3. package.json中的

```js
 
const express = require('express');
const { createProxyMiddleware } = require('http-proxy-middleware');
 
const app = express();
 
app.use('/api', createProxyMiddleware({ target: 'http://www.example.org', changeOrigin: true }));
app.listen(3000);
```

