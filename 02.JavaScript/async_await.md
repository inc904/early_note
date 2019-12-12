### async  和 await

- async作为一个关键字放到函数前面
  - 任何一个`async`函数都会隐式返回一个`promise`
- `await`关键字只能在使用`async`定义的函数中使用
  - ​    await后面可以直接跟一个 Promise实例对象
  - ​     await函数不能单独使用
- **async/await 让异步代码看起来、表现起来更像同步代码**

```js
# 1.  async 基础用法
    # 1.1 async作为一个关键字放到函数前面
	async function queryData() {
      # 1.2 await关键字只能在使用async定义的函数中使用      await后面可以直接跟一个 Promise实例对象
      var ret = await new Promise(function(resolve, reject){
        setTimeout(function(){
          resolve('nihao')
        },1000);
      })
      // console.log(ret.data)
      return ret;
    }
	# 1.3 任何一个async函数都会隐式返回一个promise   我们可以使用then 进行链式编程
    queryData().then(function(data){
      console.log(data)
    })

	#2.  async    函数处理多个异步函数
    axios.defaults.baseURL = 'http://localhost:3000';

    async function queryData() {
      # 2.1  添加await之后 当前的await 返回结果之后才会执行后面的代码   
      
      var info = await axios.get('async1');
      #2.2  让异步代码看起来、表现起来更像同步代码
      var ret = await axios.get('async2?info=' + info.data);
      return ret.data;
    }

    queryData().then(function(data){
      console.log(data)
    })s
```

