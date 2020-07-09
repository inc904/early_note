js 原生入口

```js
window.onload = function () {
  // 原生入口函数会等到DOM元素和图片全部都加载完毕后执行
  // 只能执行一次
}
```

jq 入口函数：

```js
$(function () {})

$(document).ready(function () {
  // 会等到DOM元素加载完毕就执行，不会等待图片的加载
  // 可以执行多次
})
```

符号冲突问题

```js
// $ 符号的释放
// 简单释放，之后使用 jQuery 代替
jQuery.noConflict()
// 释放后接管, 之后使用接收的符号
var tf = jQuery.noConflict()
```
