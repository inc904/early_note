```js
// store/index.js

/*
redux最核心的管理对象模块
 */
import { createStore, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'

import reducers from './reducers'

// 向外暴露store对象
export default createStore(
  reducers,
  composeWithDevTools(applyMiddleware(thunk))
)

```

```js
import { createStore, applyMiddleware, compose } from 'redux'
import reducer from './reducers' // 管理员
import thunk from 'redux-thunk'
const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
  ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
  : compose
const enhancer = composeEnhancer(applyMiddleware(thunk))
const store = createStore(
  reducer,
  // window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__() // redux
  // applyMiddleware(thunk) // thunk
  enhancer
)
export default store
```

https://github.com/zalmoxisus/redux-devtools-extension