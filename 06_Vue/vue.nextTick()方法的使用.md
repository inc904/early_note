## 基础
https://blog.csdn.net/zhouzuoluo/article/details/84752280
### 定义：
在下次DOM更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的DOM。
所以就衍生出了这个`获取更新后的DOM的Vue方法`，所以`放在Vue.$nextTick()回调函数中的执行的应该回事对DOM进行操作的js代码`

### 理解：
nextTick()，是将回调函数延迟在下一次DOM更新数据后调用，简单的理解就是：当数据更新了，在DOM渲染后，自动执行该函数。

## 什么时候需要用的 Vue.nextTick()？？

1、Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中，原因是在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。与之对应的就是mounted钩子函数，因为该钩子函数执行时所有的DOM挂载已完成。
```js
created(){
	let that=this;
    that.$nextTick(function(){  //不使用this.$nextTick()方法会报错
        that.$refs.aa.innerHTML="created中更改了按钮内容";  //写入到DOM元素
      });
  },
```
  2、当项目中你想在改变DOM元素的数据后基于新的 DOM 做点什么，对新DOM一系列的js操作都需要放进`Vue.nextTick()`的回调函数中；通俗的理解是：更改数据后当你想立即使用js操作新的视图的时候需要使用它
