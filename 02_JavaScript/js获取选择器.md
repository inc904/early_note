三、js获取兄弟节点的方式
1. 通过获取父亲节点再获取子节点来获取兄弟节点
```js
var brother1 = document.getElementById("test").parentNode.children[1];
```
2. 获取上一个兄弟节点

在获取前一个兄弟节点的时候可以使用previousSibling和previousElementSibling。他们的区别是previousSibling会匹配字符，包括换行和空格，而不是节点。previousElementSibling则直接匹配节点。

```js
var brother2 = document.getElementById("test").previousElementSibling;
var brother3 = document.getElementById("test").previousSibling;
```
3. 获取下一个兄弟节点

同previousSibling和previousElementSibling，nextSibling和nextElementSibling也是类似的。

```js
var brother4 = document.getElementById("test").nextElementSibling;
var brother5 = document.getElementById("test").nextSibling;
```