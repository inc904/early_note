## NodeJS 操作 MySQL

### 安装

```shell
npm i mysql
```

### 操作

```js
var mysql = require('mysql')
// 1. 创建连接
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'root',
  database: 'itcast',
})

// 2. 连接数据库
connection.connect()

// 3. 执行数据库操作
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error
  console.log('The solution is: ', results[0].solution)
})

// 4. 关闭连接
connection.end()
```
