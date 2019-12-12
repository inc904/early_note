## vue-resource 的使用

### 0.说明

### 1.安装

1. script 标签引入
2. npm 安装

### 2.使用

```js
// 基于全局的 Vue 对象使用 'http'
Vue.http.get('/someURL', [options])
  .then(function(){
  	// success
	}, function(){
  	// error
})
Vue.post('/someURL', [body], [options])
	.then(successCallback, errorCallback)

// 基于一个 Vue 实例内使用 '$http'
this.$http.get('/someURL', [options])
  .then(function(){
  	// success
	}, function(){
  	// error
})
```

### 3.常用请求方式
  1. get
  2. post
  3. jsonp
  4. jsonp实现原理
    - 由于浏览器安全性限制，不允许 AJAX 访问 协议不同、域名不同、端口号不同的数据接口
    - 可以通过动态常见 Script 标签的形式，把 script 标签的 src 属性，指向数据接口的地址因为 script 标签存在跨域限制，这种属性获取方式称作 JSONP 。
     （根据 JSONP 的实现原理，知晓 jsonp 只支持 get 请求）
    - 具体实现过程：
      + 现在客户端定义一个回调方法，预定义对数据的处理
      + 再把这个回调方法的名称，通过URL传参的形式，提交到服务器的数据接口
      + 服务器的数据接口组织好要发送给客户端的数据，在拿着客户端传递过来的回调方法的名称，拼接出一个调用这个方法的字符串，发送给客户端去解析执行。
      + 客户端拿到服务器返回的字符串之后，当做 Script 脚本去解析执行，这样就能够拿到JSONP的数据了。