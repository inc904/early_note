### 高阶函数

定义：将函数作为参数或者返回值是函数的的函数。

日常中常见的高阶函数：

1. 常见的 reduce、sort 等函数。
2. 返回值是函数的的函数。

```js
function add(a){
  return function function(b){
    return a + b
  }
}
var add3 = add(3)
add3(4) = 3 + 4 // true

add3(3)(4)

// add 函数 在 ES6 中的写法：
let add = a => b=> a + b
```

其实以上就是柯里化函数。

### 多个连续的箭头函数

形如：a => b => c => { xxx }

redux-thunk 源码:

```js
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => (next) => (action) => {
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument)
    }
    return next(action)
  }
}

const thunk = createThunkMiddleware()
thunk.withExtraArgument = createThunkMiddleware
export default thunk
```

> 多个连续箭头函数就是 es6 的多次柯里化的写法

### 柯里化（curried function）

> wiki 的柯里化定义:
> 把接受多个参数的函数变换成接受一个单一参数的函数，并且返回（接受余下的参数而且返回结果的）新函数的技术。

关键是理解柯里化，其实可以把它理解成，柯里化后，将第一个参数变量存储在函数里面了（闭包），然后本来需要 n 个 参数的函数就可以变成 只需要 剩下的 （n - 1 ）个参数就可以调用了，比如：

```js
let add = (x) => (y) => x + y
let add2 = add(2)
```

n 个连续箭头组成的函数实际上就是柯里化了 n - 1 次。

具体调用过程如下：

前 n - 1 次调用，其实是提前将参数传递进去，并没有调用最内层函数体，最后一次调用才会调用最内层函数体，并返回最内层函数体的返回值。

结合上文可知，这里的多个连续箭头（无论俩个箭头函数三个及以上）函数连在一起 就是在柯里化。

所以连续箭头函数就是多次柯里化函数的 es6 写法。

let test = a => b => c => {xxx}

调用特点：

let test = a => b => c => {xxx}

比如对于上面的 test 函数，它有 3 个箭头， 这个函数要被调用 3 次 test(a)(b)(c)，前两次调用只是在传递参数，只有最后依次调用才会返回 {xxx} 代码段的返回值，并且在 {xxx} 代码段中可以使用 a,b,c

#### 柯里化函数的功能

1. 可以惰性求值
2. 可以提前传递部分参数
