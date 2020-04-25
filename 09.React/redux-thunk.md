## redux-thunk

安装

```shell
yarn add redux-thunk
```

配置

```js
// store/index.js
import { createStore, applyMiddleware, compose } from 'redux'
import reducer from './reducer' // 管理员
import thunk from 'redux-thunk'

const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
  ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
  : compose
const enhancer = composeEnhancer(applyMiddleware(thunk)) // 增强函数，链式调用。为了兼容 devtool
const store = createStore(
  reducer,
  // window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__() // redux
  // applyMiddleware(thunk) // thunk
  enhancer
)
export default store

```

### 方法二：

https://www.npmjs.com/package/redux-devtools-extension

```js
import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'
import reducers from './reducers'

const store = createStore(reducers, composeWithDevTools(applyMiddleware(thunk)))
export default store

```

