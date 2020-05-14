## Promise 基本用法

- 首先实例化 Promise 对象，构造函数中传递函数，该函数中用于处理异步任务。
- resolve 和 reject 两个参数用于处理成功和失败两种情况，并通过 p.then() 获取处理结果。

```js
let p = new Promise(function (resolve, reject) {
  // 成功时调用 resolve()
  // 失败时调用 reject()
})
p.then(
  function (ret) {
    // 从 resolve 中得到成功的结果
  },
  function (err) {
    // 从 reject 中得到错误信息
  }
)
```

```js
/*
1. Promise基本使用
 我们使用new来构建一个Promise  Promise的构造函数接收一个参数，是函数，并且传入两个参数：  resolve，reject， 分别表示异步操作执行成功后的回调函数和异步操作执行失败后的回调函数
*/

var p = new Promise(function (resolve, reject) {
  //2. 这里用于实现异步任务  setTimeout
  setTimeout(function () {
    var flag = false
    if (flag) {
      //3. 正常情况
      resolve('hello')
    } else {
      //4. 异常情况
      reject('出错了')
    }
  }, 100)
})
//  5 Promise实例生成以后，可以用then方法指定resolved状态和reject状态的回调函数
//  在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了
p.then(
  function (data) {
    console.log(data)
  },
  function (info) {
    console.log(info)
  }
)
```

## promise 处理 ajax 请求

```js
 /*
      基于Promise发送Ajax请求
    */
function queryData(url) {
    #   1.1 创建一个Promise实例
    var p = new Promise(function(resolve, reject){
        var xhr = new XMLHttpRequest();
        xhr.onreadystatechange = function(){
            if(xhr.readyState != 4) return;
            if(xhr.readyState == 4 && xhr.status == 200) {
                # 1.2 处理正常的情况
                resolve(xhr.responseText);
            }else{
                # 1.3 处理异常情况
                reject('服务器错误');
            }
        };
        xhr.open('get', url);
        xhr.send(null);
    });
    return p;
}
# 注意：  这里需要开启一个服务
# 在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了
queryData('http://localhost:3000/data')
    .then(function(data){
    console.log(data)
    #  1.4 想要继续链式编程下去 需要 return
    return queryData('http://localhost:3000/data1');
})
    .then(function(data){
    console.log(data);
    return queryData('http://localhost:3000/data2');
})
    .then(function(data){
    console.log(data)
});
```

## Promise 基本 API

### 实例方法

- then()

  得到异步任务返回的结果，处理正确的结果或者直接将错误信息返回。

- catch()

  获取异常信息，使用 catch 的时候，将不在需要在 then 中处理错误的信息。

- finally()

  成功与否都会执行（不是正式标准）。

```js
/*
      Promise常用API-实例方法
    */
    // console.dir(Promise);
    function foo() {
      return new Promise(function(resolve, reject){
        setTimeout(function(){
          // resolve(123);
          reject('error');
        }, 100);
      })
    }
    // foo()
    //   .then(function(data){
    //     console.log(data)
    //   })
    //   .catch(function(data){
    //     console.log(data)
    //   })
    //   .finally(function(){
    //     console.log('finished')
    //   });

    // --------------------------
    // 两种写法是等效的
    foo()
      .then(function(data){
        # 得到异步任务正确的结果
        console.log(data)
      },function(data){
        # 获取异常信息
        console.log(data)
      })
      # 成功与否都会执行（不是正式标准）
      .finally(function(){
        console.log('finished')
      });
```

### 静态方法

- all()

  `Promise.all`方法接受一个数组作为参数，数组中的对象（p1，p2，p3）均为 Promise 实例（如果不是一个 Promise ，该项会被 `Promise.resolve` 转换为一个 Promise）。他的状态由这三个 Promise 实例决定。

- race()

  `Promise.race` 方法同样接收一个数组作为擦拿书。当 p1，p2，p3 中有一个实例的状态发生变化（改为 fulfilled 或 rejectd），p 的状态就会跟着改变。并把第一个改变的 Promise 的返回值，传给 p 的回调函数。

```js
/*
      Promise常用API-对象方法
    */
// console.dir(Promise)
function queryData(url) {
  return new Promise(function (resolve, reject) {
    var xhr = new XMLHttpRequest()
    xhr.onreadystatechange = function () {
      if (xhr.readyState != 4) return
      if (xhr.readyState == 4 && xhr.status == 200) {
        // 处理正常的情况
        resolve(xhr.responseText)
      } else {
        // 处理异常情况
        reject('服务器错误')
      }
    }
    xhr.open('get', url)
    xhr.send(null)
  })
}

var p1 = queryData('http://localhost:3000/a1')
var p2 = queryData('http://localhost:3000/a2')
var p3 = queryData('http://localhost:3000/a3')
Promise.all([p1, p2, p3]).then(function (result) {
  //   all 中的参数  [p1,p2,p3]   和 返回的结果一 一对应["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
  console.log(result) //["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
})
Promise.race([p1, p2, p3]).then(function (result) {
  // 由于p1执行较快，Promise的then()将获得结果'P1'。p2,p3仍在继续执行，但执行结果将被丢弃。
  console.log(result) // "HELLO TOM"
})
```
