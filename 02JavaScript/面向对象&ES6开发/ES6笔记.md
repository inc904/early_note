## ES兼容性

[ES5兼容性](http://kangax.github.io/compat-table/es5/)
[ES6兼容性](http://kangax.github.io/compat-table/es6/)
IE10、Chrome、Firefox、移动端、NodeJS

## 编译和转换

1. 在线转化

2. 提前编译
   
## es6中的语法

### 新的声明方法
- js的语法性质
  
  1. 可以重复声明
     
      var a = 12;
      var a = "hello";
  
  2. 可控制修改
     
      var GIT_HOST = "github.com"
      if(GIT_HOST = "git"){
     
      }
      ES5 中不会报错，但是使用ES6 中 let 声明的变量会报错
  
- let        防止重复声明  变量（可以重新赋值）

- const     防止重复声明  常量（不可重新赋值）
  
     
  
     新的声明方式解决了 重复声明 和 控制修改

### 块级作用域

3. 块级作用域：
   
    闭包：js中的变量没有块级作用域的情况下的临时解决方案。一旦有了块级作用域之后，就不在需要闭包了。

ES5 中 var 的作用域是函数级的，在函数里面任何地方定义i，都是等价的 。

ES6 中 let 的作用域是块级的，{}，花括号代码块中的

### 解构赋值

1、两边的结构必须一样

```js
let {a,b} = [12, 6]  ---->  ✖
```
2、右边必须是个东西

```js
let {a, b} = {12, 5}  ----> ✖
```

3、解构 和 赋值  必须同时完成

```js
let {a, b};
{a, b} = {a : 12, b : 5}  ----> ✖
```



### 箭头函数和this

```js
function(){
  // code...
}
() => {}
```

简写：
    1、如果有且只有一个参数,()可以不写
    2、如果有且仅有一句话并且是return ，｛｝也可以不写

    修正this：    

#### 参数扩展：

- 收集
  
  ```js
  function show(a, b, ...c){
      console.log(a,b,c)
  }
  show(12,7,89,20,0,1);
  //result: a=12,b=7,c=[89,20,0,1]
  ```
  
- 展开:

  ```js
  let arr = [1, 2, 3]
  // ...arr
  // 1,2,3
  let arr2 = [4, 5, 6]
  let arr3 = [...arr, arr2] // => arr3 = [1, 2, 3, 4, ,5, 6]
  ```
  
- 默认参数

  ```js
  function fn(a, b = 5) {}
  fn(1, 2)
  // 如果b 没有传值，就采用默认参数的值5
  ```

  

- 数组展开，

- json展开



### 数组

- Array扩展：map、reduce、filter、forEach
  
 ```js
## map 映射 : 一一对应

let arr = [12,5,8]
let arr2 = arr.map(item =>
                   return item * 2
                  )
// arr2 => [25, 10, 16]

[67,122,36,59] => [及格,及格,不及格,不及格]
let score = [67,122,36,59]
let stu = score.map( item => {
    return item > 60 ? '及格' : '不及格'
})
// stu =>  [及格,及格,不及格,不及格]
## reduce: 汇总； 一堆出来一个，n => 1 减少

// 总数
[12, 67, 8912, 213] => 
let arr = [12, 67, 8912, 213]
let res = arr.reduce((tmp, item, index ) => {
    return tmp + item 
})
res => 总和


// 算平均分

let res = arr.reduce((tmp, item, index ) => {
    if(index != arr.length - 1){
    	return tmp + item    
    }else {
        return (tmp + item)/arr.length
    }
})
res => 平均数

## filter 过滤

let arr = [12, 5, 6, 9, 7]
let res = arr.filter( item => {
   return item % 3 == 0
})
## forEach 没有返回值  遍历（迭代）


 ```

### 字符串

- startsWith() / endsWith()

- 模板字符串：
- json写法、json对象

### 面向对象

#### 基础

#### 实例

#### json

#### promise

## babel.js 编译

1. 安装 node.js ,初始化 项目
   
   > npm init -y

2. 安装 babel-cli
   
   > npm i @babel/core @babel/cli @babel/preset-env -D
   > npm i @babel/polyyfill -S  // 填充，编译的过程中。检测目标平台的支持

3. 添加执行脚本
   
   ```json
    "script": {
        "bulid" : "babel src -d dest" 
    }
    // 把src文件夹里面的ES6编译成ES5到dest文件夹中
   ```

4. 添加 .babellrc 配置文件
   
   ```
    "presets" : ["@babel.preset-env"]
   ```

5. 执行编译
   
   > npm run bulid 


