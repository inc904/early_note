使用的时候注意以下几点：

- 判断是否是在开发环境，只在开发环境添加此调试工具

- 新建store的时候需要判断window.devToolsExtension值是否存在

- 使用redux的compose方法结合redux中间件和devToolsExtension

  ```js
  import { createStore, applyMiddleware, compose } from 'redux';
  let middlewares = [];
  let storeEnhancers;
  if(process.env.NODE_ENV==='production'){
    storeEnhancers = compose(
        applyMiddleware(...middlewares,sagaMiddleware)
    );
  }else{
    storeEnhancers = compose(
        applyMiddleware(...middlewares,sagaMiddleware),
        (window&& window.devToolsExtension) ? window.devToolsExtension() : (f) => f,
    );
  }
  const store = createStore(reducer, initialState={} ,storeEnhancers);
  
  ```

  