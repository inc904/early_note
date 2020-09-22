## Redux

Redux = Reducer + Flux

#### 使用

1. 安装

   ```shell
   npm i redux -S
   ```

2. mkdir store； create index.js；

   ```js
   // index.js
   import { createStore } from 'redux'
   import reducer from './reducer' // 引入记录本，作为参数，传给 store
   const store = createStore(reducer) // store：管理员 
   export default store
   ```

3. create reducer.js ;

   ```js
   const defaultState = {
        inputValue: '',
     	list: []  // 存储值
   } // 默认笔记本上什么没有存储
   export default (state = defaultState , action) => {  // 返回一个函数 reducer：记录本，所有书籍信息
     return state
   }
   
   ```

   

4. 组件中创建事件

   ```js
   // TodoList.js 
   handleInputChange = e => {
       const action = {  // 创建一个action
         type: 'change_input_value',
         value: e.target.value
       }
       store.dispatch(action) // 把 action 传递给 store ，store 会自动把 action 传给记录本 reducer 处理
     }
   ```

5. 在 reducer 中，接收并处理

   ```js
   // reducer.js
   export default (state = defaultState, action) => {
     console.log(state, action) // 可以拿到之前的 数据 和 action
     if (action === 'change_input_value') {
       const newState = JSON.parse(JSON.stringify(state)) // 对之前的数据进行深拷贝
       newState.inputValue = action.value // 把最新的数据 赋值给 新数据对象
       return newState // 把 新的 state 返回给 store，因为 reducer 可以接收 state，但是绝不能修改 state
     }
     return state
   }
   
   ```

6. 组件中的操作

   ```js
   // TodoList.js
   constructor(props){
       store.subscribe(this.handleStoreChange) // 订阅 store 的改变
   }
   handleStoreChange = ()=>{
       this.setState(store.getState()) // 查询到 state 改变之后，把新的值 通过 store的getState 方法查询到 store 中的最新数据，重置 赋值给 组件中的 state
   }
   
   // 此时就可以更改页面上的数据了
   ```

   

#### 优化

##### actionTypes.js 统一管理 actionType

在组件中不断的创建 action，reducer 中 接收不同的 action，两处的 action.type 必须相同才能进行相应的逻辑处理。

所以，我们把 action.type 抽离出来。

cd store ; create actionTypes.js

```js
// actionTypes.js
export const CHANGE_INPUT_VALUE = 'change_input_value'
export const ADD_TODOITEM = 'add_todoItem'
export const DELETE_TODOITEM = 'delete_todoItem'

```

之后在 组件 中和 reducer.js 中 我们进引入 常量 进行 处理。

```js
action.type = ADD_TODOITEM
```

##### actionCreators.js  统一创建 action

```js
// actionCreators.js  

import {
  CHANGE_INPUT_VALUE,
  ADD_TODOITEM,
  DELETE_TODOITEM
} from './actionTypes'
export const getInputChangeValueAction = value => ({
  type: CHANGE_INPUT_VALUE,
  value
})
export const addnewItemAction = () => ({
  type: ADD_TODOITEM
})
export const deleteItemAction = index => ({
  type: DELETE_TODOITEM,
  value: index
})

```

在组件中 

```js
// TodoList.js
import {
  getInputChangeValueAction,
  addnewItemAction,
  deleteItemAction
} from './store/actionCreators'
// 在创建 action 时候，我们就可以通过 actionCreator 中的方法 ，统一进行创建了
  handleInputChange = e => {
    console.log(e.target.value)
    // const action = {
    //   type: CHANGE_INPUT_VALUE,
    //   value: e.target.value
    // }
    const action = getInputChangeValueAction(e.target.value)
    store.dispatch(action)
  }
  handleAddItem = () => {
    // const action = {
    //   type: ADD_TODOITEM
    // }
    const action = addnewItemAction()
    store.dispatch(action)
  }
  handleDeleteItem = index => {
    console.log('delete action', index)
    // const action = {
    //   type: DELETE_TODOITEM,
    //   value: index
    // }
    const action = deleteItemAction(index)
    store.dispatch(action)
  }
```



