## 命令行操作 MongoDB

### 启动和关闭

```shell
# 默认使用执行 mongod 命令所处盘符的根目录下的 /data/db 座位自己的数据存储目录， 所以首次启动需要手动创建 /data/db 目录
# 启动
mongod
# 关闭
# ctrl + c 或者 直接 关闭终端窗口
# 修改 默认数据存储命令
mongod --dbpath = 数据存储目录路径
```

### 连接和退出

```shell
# 默认连接本机的 MongoDB 服务
mongo
# 退出z
exit
```

### 基本命令

```shell
# 查看当前数据库列表
show dbs
# 创建数据库

# 查看当前连接的数据库，如果没有连接，会自动切换到 test 数据库，但是没有数据，当插入数据后，可以使用 show dbs 命令查看到 test 数据库
db
# 切换到指定数据库，如果没有会新建
use DBName
# 创建表, cname 集合名, 插入一行数据
db.cname.insertOne({"name": "jack"})
# 查看当前db的所有集合（表）
show collections
# 查看 当前表的 数据
db.cname.find()

```

## node 中操作 MongoDB

### 官方包，较为繁琐

`npm i mongodb`

### mongoose 第三方包，基于官方包，再一次封装，较简洁

`npm i mongoose`

## mongoose 指南

### 1.设计 Schema 发布 Model

```javascript
var mongoose = require('mongoose')

var Schema = mongoose.Schema
// 1.连接数据库
// 如果自定的数据库不存在，当你插入第一条数据的时候会自动被创建出来
mongoose.connect('mongodb://localhost/itcast', { useNewUrlParser: true })

// 2.设计文档结构（表结构）
// 字段名称就是 结构中的 属性名称
// 约束的目的 是为了数据的完整性，不要有脏数据
var blogSchema = new Schema({
  title: {
    type: String,
    required: true,
  },
  author: String,
})

// 3.mongoose.model() 方法就是将一个 架构 发布 为 model
// 第一个参数： 传入一个首字母大写的数字字符串来表示你的数据库的名称
// mongoose 会自动江湖大写名词的字符串 生成 小写复数 的集合名称
// 这里的 Blog 最终会变成 blogs 集合 名称
// 第二个参数： 架构 Schema
// 返回值 模型构造函数
var Blog = mongoose.model('Blog', blogSchema)
```

### 2.操作数据（增删改查）

```js
// 4. 操作集合 blogs 中的数据
// 新增数据
// var article = new Blog({
//   title: 'notnot',
//   author: 'zhangsan'
// })

// article.save(function(err, ret){
//   if (err) {
//     console.log('保存失败')
//   }else {
//     console.log('保存成功')
//     console.log(ret)
//   }
// })
// 查询数据

// 查询所有
Blog.find(function (err, data) {
  if (err) {
    console.log('查询失败')
  }
  console.log('查询成功')
  console.log(data)
})

// 条件查询
// Blog.find({title: 'first article'}, function (err, data) {
//   if (err) {
//     console.log('查询失败')
//   }
//   console.log('查询成功')
//   console.log(data)
// })

// 查询单个，只返回查询到的第一个数据

// Blog.findOne({title: 'first article'}, function (err, data) {
//   if (err) {
//     console.log('查询失败')
//   }
//   console.log('查询成功')
//   console.log(data)
// })

// 删除数据
// Blog.remove({title: 'notnot'}, function(err,data){
//   if(err) {
//     console.log('delete error')
//   }
// })
// 修改数据
// Blog.findOneAndUpdate({title: 'notnot'}, { title: 'goodgood'},function(err, data){
//   if(err){
//     console.log('update error')
//   }
//   console.log('success',data)
// })
// = other methods =
// Blog.findByIdAndUpdate()
```
