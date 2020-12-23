# SPA

single page application的缩写。单页面应用程序，或者单页web应用。

页面 URL 构成：

`http://www.babala.com/index.html?name=jack&old=32#mylove/is/world/peace`

如上的 URL 由以下部分构成：

- `http://`  规定了 页面 采用的 协议
- `www.babala.com`  为页面所属的域名
- `index.html `为读取文件的名称
- `?name=jack&old=32 ` 给页面通过 GET 传递的参数
- `#mylove/is/world/peace` 为页面的锚点区域

前面四个发生改变得时候，会触发浏览器的跳转或者是刷新行为，而更改 URL 中的锚点并不会出现这种行为。所以 几乎 所有 SPA 应用 都是都过这个特性来实现路由的跳转。以 vue 为例，他的本地 URL 结构一般是下面这种格式：

`http://localhost:8080/#/settings/task`

所谓的路由地址就是在`#`符号后面，也就是利用了锚点的特性。