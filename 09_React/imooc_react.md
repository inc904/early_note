##  基础

### React Fiber

 16版本及16版本中的一些底层实现

### 选择Vue 或 React

React 灵活性，复杂的业务

Vue 更丰富API，灵活性有限制，更面向用户的选择

### serviceWorker 

PWA ：progressive web application

把页面放到缓存中

`import * as serviceWorker from './serviceWorker';`



### immutable 思想

state 不允许我们做任何的修改

Immutable Data 就是一旦创建，就不能再被更改的数据。

### 代码优化

#### 关于再 render 函数中渲染 this.props.xxx 或者 this.state.xxx

```js
props: {
    type: 'stringType',
    name: "jack" 
}
state: {
    value: '123',
    list: [1,2,3]
}
// 原始用法
<div type={this.props.type}  name={this.props.name}/>
<div value={this.state.type}  list={this.state.name}/>
// 优化写法,通过解构赋值，先保存下来
let {type, name} = this.props
let {value, list: bookList} = this.state // 解构的时候 可以重新命名
// 优化用法
<div type={type}  name={name}/>
<div value={type}  list={booklist}/>
```



#### bind 修改 this 指向的时候

原始写法：是再绑定事件的时候，用 bind 修改 this 指向；

优化写法：bind 改变 this 指向的操作，可以提前在 组件的 constructor 中实现；

我的写法：习惯在定义 事件的时候，采用 函数表达式 + 箭头函数 

#### setState 异步方法

```js
handle_1(){
    this.setState({
        name: "ming"
    })
}
handle_2(){
    this.setState({
        name: this.state.name
    })
}
// good
handle_1_good(){
    this.setState(() => ({name: "ming"}))
}
handle_2_good(){
    this.setState((prevState) => ({
        name: prevState.name
    })
}
```

### 生命周期

生命周期函数是指子啊某一个时刻组件会自动执行的函数。 

#### 在子组件的  shouldComponentUpdate 中，判断是否需要更新子组件

```js
shouldComponentUpdate(nextProps, nextState){ // 接收两个参数
    if(nextProps.xxx !== this.props.xxx){
        return true
    }
    return false
}
```

#### 在 componentDidMount 中发送 Ajax 请求



### 过渡和动画

- 切换 className， 写样式
- react-transition-group  

### UI组件和容器组件的拆分

### 无状态组件

## 中间件

### redux-thunk

#### redux-thunk的配置:

使得调用 thunk 的同时，也可以正常使用 redux-dev-tool

```js
// store/index.js

import { createStore, applyMiddleware, compose } from 'redux'
import ReduxThunk from 'redux-thunk'

import reducer from './reducer'
const reduxConfig =
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
  ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
  : compose
const enhancer = composeEnhancers(applyMiddleware(ReduxThunk))
const store = createStore(reducer, enhancer)
export default store

```

#### 在组件中应用

之后我们可以讲之前在 componentDidMount 中定义的 ajax 请求，放到 actionCreator.js 中处理。

```js
// TodoList.js 组件中的请求
 componentDidMount() {
     axios
       .get('https://jsonplaceholder.typicode.com/todos?_limit=5')
       .then(res => {
         const data = res.data
         const action = initListAction(data) // 以前的 action 只能是 一个对象，引用了 thunk 之后，可以是 函数了
         store.dispatch(action)
       })
    const action = getTodoListData() // 在 actionCreator 中创建的 action
    console.log(action)
    store.dispatch(action)
  }
```

#### 在actionCreator.js 中进行配置

```js
// actionCreator.js
export const getTodoListData = () => {
  return dispatch => { // 直接接收 一个 dispatch 参数，调用的时候不用加 store 了
    axios
      .get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => {
        const data = res.data
        const action = initListAction(data)
        dispatch(action)
        // console.log(data)
      })
  }
}
```

### redux-saga

#### redux-saga 的配置

```js
// store/index.js
import { createStore, applyMiddleware, compose } from 'redux'
import createSagaMiddleware from 'redux-saga'
import reducer from './reducer'
import TodoSagas from './sagas' ##
const reduxConfig =
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()

// create the saga middleware
const sagaMiddleware = createSagaMiddleware() ##

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__
  ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})
  : compose
const enhancer = composeEnhancers(applyMiddleware(sagaMiddleware)) ##
const store = createStore(reducer, enhancer)

// then run the saga
sagaMiddleware.run(TodoSagas) ##
export default store

```

#### create sagas.js 

```js
// sagas.js 

function* mySaga() {
  // yield takeLatest("USER_FETCH_REQUESTED", fetchUser);
}

export default mySaga

```

#### 把 componentDidMount 中的请求，放到 sagas.js 文件中请求

在 todolist 组件中,创建派发了一个action

```js
componentDidMount() {
    const action = getInitSagaAction()
    store.dispatch(action)
    console.log('saga', action)
}
```

之前在创建 store 的时候，使用了 saga 中间件，进行了基础的配置，

- 引入`createSagaMiddleware`

- 创建一个 `SagaMiddleware`: `const sagaMiddleware = createSagaMiddleware()`

- 使用 这个 middle ware：

  ```js
  const enhancer = composeEnhancers(applyMiddleware(sagaMiddleware))
  ```

- 创建 sagas.js并引入，`run`起来

  ```js
  // then run the saga
  sagaMiddleware.run(TodoSagas)
  ```

- 编写 sagas 文件，一定要导出了个 generator 函数；在这个 函数中，写了一些 判断 type 的逻辑

- 匹配到 type ，执行方法，在这个方法中，创建一个 action， 派发给 store， store 传递给 reducer ，然后 reducer 判断到 type = init... , 就会执行 更新 list，然后更新 state

然后不仅仅 reducer 能接收到 这个 action，还有 sagas.js 中的 mySaga 函数   也能接收到这个 action。然后通过 takeEvery 这个函数，声明了 ，如果接收到 类型 为 `GET_INIT_LIST_SAGA`的 action，就执行第二个参数的 方法 fetchInitList， 然后就会执行这个方法，然后就可以将异步的一些逻辑写在这里，就实现了 我们想要将 异步 逻辑 拆分到 sagas 文件中管理的 需求。

```js
import { takeEvery, put } from 'redux-saga/effects'
import { GET_INIT_LIST_SAGA } from './actionTypes'
import axios from 'axios'
import { initListAction } from './actionCreators'

function* fetchInitList() {
  console.log('abc')
  // axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5').then(res => {
  //   const data = res.data
  //   const action = initListAction(data)
  //   // store.dispatch(action)
  //   put(action)
  // })

  // const res = yield axios.get(
  //   'https://jsonplaceholder.typicode.com/todos?_limit=5'
  // )
  // const action = initListAction(res.data)
  // yield put(action)

  try {
    const res = yield axios.get(
      'https://jsonplaceholder.typicode.com/todos?_limit=5'
    )
    const action = initListAction(res.data)
    yield put(action)
  } catch (e) {
    console.log('请求失败')
  }
}
// generator 函数
function* mySaga() {
  yield takeEvery(GET_INIT_LIST_SAGA, fetchInitList)
}

export default mySaga

```

## react-redux



```js
// src/index.js
import React from 'react'
import ReactDOM from 'react-dom'
import TodoApp from './TodoApp'
import { Provider } from 'react-redux'  # 提供器
import store from './store'

const App = (
  <Provider store={store}>
    <TodoApp />
  </Provider>
)

ReactDOM.render(App, document.getElementById('root')) 

```



```js
// store/index.js
import { createStore } from 'redux'
import reducer from './reducer'
const store = createStore(reducer)
export default store

```



```js
// TodoList.js
import React, { Component } from 'react'
import { Input, Button, List } from 'antd'
import 'antd/dist/antd.css'
// import store from './store'
import { connect } from 'react-redux'

class TodoApp extends Component {
  // constructor(props) {
  //   super(props)
  //   this.state = store.getState()
  // }

  render() {
    return (
      <div style={{ margin: '20px' }}>
        <Input
          style={{ width: '300px', marginRight: '10px' }}
          placeholder="add new todo"
          value={this.props.inputValue}
          onChange={this.props.handleInputChange}
        ></Input>
        <Button type="primary">添加</Button>
        <List
          style={{ width: '300px', marginTop: '10px' }}
          bordered
          dataSource={[]}
          renderItem={(item, index) => {
            return <List.Item onClick={() => {}}>123</List.Item>
          }}
        />
      </div>
    )
  }
}
const mapStateToProps = state => {
  # 连接规则，把 state 中的数据 映射成组件的 props
  return {
    inputValue: state.inputValue,
    list: state.list
  }
}
const mapDispatchToProps = dispatch => {
  # store.dispatch 映射到 props 上
  return {
    handleInputChange(e) {
      console.log(e.target.value)
      const action = {
        type: 'change_input_value',
        value: e.target.value
      }
      dispatch(action)
    }
  }
}
export default connect(mapStateToProps, mapDispatchToProps)(TodoApp) # 连接器

```



```js
// reducer.js
const defaultState = {
  inputValue: 'hello',
  list: ['world']
}
export default (state = defaultState, action) => {
  if ((action.type = 'change_input_value')) {
    const newState = JSON.parse(JSON.stringify(state))
    newState.inputValue = action.value
    return newState
  }

  return state
}

```

