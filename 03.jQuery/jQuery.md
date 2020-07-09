# jQuery 笔记

## 事件

#### 事件委派

```js
$('ul').delegate('li', 'click', function () {
  // code
})
$('ul').on('li', 'click', function () {
  // code
})
$('ul').bind('li', 'click', function (event) {
  // code
  var target = $(event.target)
  if (target.prop('nodeName') == 'LI') {
    target.css('background-color', 'red')
  }
})
```
