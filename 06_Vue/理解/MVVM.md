## MVC

model,view,controller 模型、视图、控制器

Java： springMVC

PHP： smarty

Node： Express、Koa

### modal：

在 mvc 中实际是`数据模型`的概念，可以把它当成`从数据库中查询出来的一条数据，或者是将查询出的元数据经过裁剪或者处理后的一个特定的数据模型结构`。

### controller:

是数据模型与 VIew 视图之间的桥梁层，`实际界面层的各种变化都要经过他来控制`，而且从界面提交的数据，也会经过 controller 的组装检查生成数据模型，然后改变数据库里的数据内容。

### MVC 的使用

数据到页面的渲染：先要查询数据库后，将拿到的元数据进行一些处理，（删除无效字段，或者进行多哥数据模型间的数据聚合，然后在给到模板引擎，进行数据组装），最后组合完成进行渲染后生成 HTML 格式文件供文件浏览器使用。

前后端分离 ==> view 层 ==> Restful 风格的接口 兴起

前后端分离之后，可以理解成整个系统在原先的 MVC 基础上 View 层进行细化，把真格前端项目当成一个 View 层，从前端角度看， Restful 接口返回的 JSON 数据当成一个数据模型，作为 MVC 的 Model 层。而前端 JavaScript 自身对数据的处理是 controller 层， 真正的页面渲染结果是 View 层。

下例以前端视角，MVC 模式。接口返回的数据 Model 模型与 View 页面之间由 controller 连接，来完成系统中的数据展示。

```html
<div>
  <span id="name"></span>
  <div id="data"></div>
</div>
```

```js
// 生成 model 数据模型
function getDataApi() {
  // 模拟 接口返回
  return {
    name: 'mvc',
    data: 'mvc 中的数据',
  }
}
// controller 控制逻辑
function pageController() {
  const res = getDataApi()
  $('#name').text(`姓名：${res.name}`)
  $('data').text(res.data)
}
```

## MVVM

MVVM 是 Model-View-ViewModel 的缩写。

- M：Model 数据模型，也可在 Model 中定义数据修改和操作业务逻辑。
- V：view 代表UI组件，负责将数据模型转化成UI呈现出来。
- VM：ViewModel 监听数据模型的改变和控制试图行为、处理用户交互，简单理解就是一个同步 VIew 和 Model 的对象。连接 Model 和 View。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。



**ViewModel** 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

前端对于逻辑的控制越来越轻量，mvvm 模式作为 mvc 模式的一种补充出现了，最终的目的都是`将Model里的数据展示到view视图上`，而 mvvm 相比于 mvc 则将前端开发所要控制的逻辑更加轻量级。

### ViewModel

将模型与视图做了一层绑定关系，在理想情况下，数据模型返回什么视图就应该展示什么。

```html
<div>
  <span vm-bind-key="name"></span>
  <div vm-bind-key="data"></div>
</div>
```

```js
// 生成数据 model 模型
function getDataApi() {
  // 模拟接口返回
  return {
    name: 'mvc',
    data: 'mvc 的数据信息',
  }
}
// viewModel 控制逻辑
function pageViewModel() {
  const res = getDataApi()
  return res
}
```

理想情况下，在 viewModel 引入之后，视图完全由接口返回数据驱动。

在 mvvm 模式下，controller 控制逻辑不是没有了，想操作 DOM 相应的逻辑被 SDK（vue 内部封装实现）统一实现了，像不操作接口返回的数据是因为服务端在数据返回给前端前已经操作好了。

pageModel 函数实现了，如何将数据模型和页面视图绑定起来？

1. Angular 的 主动轮询检查新旧值的变化更新视图
2. Vue 利用 ES5 的 OBject.defineProperty 的 getter/setter 方法绑定，
3. backbone 的发布订阅模式

从主动和被动的方式，实现了 viewModel 的关系绑定。

### Vue2.0 MVVM 实现

当 Object.defineProperty 方法在给数据 Model 对象定义属性的时候先挂载一些方法，在这些方法里实现与界面的值的绑定响应关系，当应用的属性被读取或者写入的时候便会触发这些方法，从而达到数据模型里的值发生变化时同步响应到页面上。

```html
<div id="app">
  <span>{{name}}</span>
  <span>{{data}}</span>
</div>
<script src="vue.js"></script>
```

```js
// 生成 model 数据模型
function getDataApi() {
  // 模拟接口返回
  return {
    name: 'mvc',
    data: 'mvc 数据信息',
  }
}
new Vue({
  el: '#app',
  data() {
    return {
      name: '',
      data: '',
    }
  },
  mounted() {
    const res = getDataApi()
    this.name = res.name
    this.data = res.data
  },
})
```

当 Vue 在实例化的时候，首先将 data 方法里返回的对象属性都挂载上 setter 方法，而 setter 方法里将页面上的属性进行绑定，当页面加载时，浏览器提供 DOMContentloader 事件触发之后，调用 moutned 挂载函数，开始获取接口数据，获取完成后给 data 里的属性赋值，赋值的时候触发之前挂载好的 setter 方法，从而引起页面的联动，达到响应式效果。

#### 简易实现 Object.defineProperty 的绑定原理

```html
<span id="name"></span>
```

```js
// Data Bindings
Object.defineProperty(data, 'name', {
  get: function () {},
  set: function (newValue) {
    // 页面响应处理
    $('#name').text(newValue)
    data.name = newValue
  },
  enumerable: true,
  configurable: true,
})
// 页面DOM listener
$('#name').onchange = function (e) {
  data.name = e.target.value
}
```

### Vue3.0 版本的 MVVM

Vue3.0 中最新的实现方式，用 Proxy 和 Reflect 来代替 Object.difineProperty。

#### Proxy

是 ES6 里的新构造函数，他的作用就是代理，简单理解为有一个对象，不想完全对外暴露出去，想做一层在亚原生对象操作之前的拦截、检查、代理，这时候就要考虑 Proxy。

```js
const myObj = {
  _id: '我是myObj里的Id',
  name: 'mvvm',
  age: 17,
}
const myProxy = new Proxy(myObj, {
  get(target, propKey) {
    if (proKey === 'age') {
      console.log('年龄私密，禁止访问！')
      return '*'
    }
    return target[propKey]
  },
  set(target, propKey, value, receiver) {
    if (propKey === '_id') {
      console.log('Id 无权修改')
      return
    }
    target[propKey] = value + (receiver.time || '')
  },
  // setPrototypeOf(target, proto) {},
  // apply(target, object, args) {},
  // construct(target, args) {},
  // defineProperty(target, propKey, propDesc) {},
  // deleteProperty(target, propKey) {},
  // has(target, propKey) {},
  // ownKeys(target) {},
  // isExtensible(target) {},
  // preventExtensions(target) {},
  // getOwnPropertyDescriptor(target, propKey) {},
  // getPrototypeOf(target) {},
})
```

```js
myProxy._id = 23
console.log(`age is:${myProxy.age}`)

myProxy.name = 'my name is Proxy'

console.log(myProxy)

const newObj = {
  time: `[${new Date()}]`,
}

Object.setPrototypeOf(myProxy, newObj)

console.log(myProxy.name)

/**
 *  id 无权修改
 *  年龄私密，禁止访问！
 *  age is : *
 *  {_id: '我是myObj的Id', name: 'my name is Proxy', age: 17}
 *  my name is newObj [Thu Mar 19 2020 18:33:22 GMT+0800 (GMT+08:00)]
 */
```

#### Reflect

Reflect 是 ES6 里的新的对象，非构造函数，不能用 new 操作符。可以把它跟 Math 类比，Math 是处理 JS 中数学问题的方法函数集合，Reflect 是 JS 中对象操作方法函数集合，它暴露出来的方法与 Object 构造函数所带的静态方法大部分重合，实际功能也类似，Reflect 的出现一部分原因是想让开发者不直接使用 Object 这一类语言层面上的方法，还有一部分原因也是为了完善一些功能。Reflect 提供的方法还有一个特点，完全与 Proxy 构造函数里 Hander 参数对象中的钩子属性一一对应。

```js
const myObj = {
  _id: '我是myObj里的Id',
  name: 'mvvm',
  age: 17,
}

const myProxy = new Proxy(myObj, {
  get(target, propKey) {
    if (propKey === 'age') {
      console.log('年龄很私密，禁止访问')
      return '*'
    }
    return target[propKey]
  },
  set(target, propKey, value, receiver) {
    if (propKey === '_id') {
      console.log('id无权修改')
      return
    }
    target[propKey] = value + (receiver.time || '')
  },
  setPrototypeOf(target, proto) {
    if (proto.status === 'enable') {
      Reflect.setPrototypeOf(target, proto)
      return true
    }
    return false
  },
})

const newObj = {
  tmie: `[${new Date()}]`,
  status: 'disable',
}

// 原对象 原型链 赋值
const result1 = Reflect.setPrototypeOf(myObj, {
  tmie: `[${new Date()}]`,
  status: 'sable',
})

myProxy.name = 'first set name'
console.log(result1) // false
console.log(myProxy.name) // first set name

// 原对象 原型链 赋值
const result2 = Reflect.setPrototypeOf(myProxy, {
  tmie: `[${new Date()}]`,
  status: 'sable',
})

myProxy.name = 'second set name'
console.log(result2) // true
console.log(myProxy.name) // //second set name [Thu Mar 19 2020 19:43:59 GMT+0800 (GMT+08:00)]

/*当执行到这里时直接报错了*/
// 原对象原型链赋值
Object.setPrototypeOf(myProxy, {
  time: ` [${new Date()}]`,
  status: 'disable',
})
myProxy.name = 'third set name'
console.log(myProxy.name)
/**
 * 报错
 */
```

解释一下上面的这段代码，通过 Reflec.setPrototypeOf 方法修改原对象原型时，必须经过 Proxy 里 hander 的挂载的 setPrototypeOf 挂载函数，在挂载函数里进行条件 proto.status 是否是 enable 筛选后，再决定是否真正修改原对象 myObj 的原型，最后返回 true 或者 false 来告知外部原型是否修改成功。

这里还有一个关键点，就是在代码执行到原有的 Object.setPrototypeOf 方法时，程序则直接抛错，这其实也是 Reflect 出现的一个原因，即使现在 ES5 里的 Object 有同样的功能，但是 Reflect 实现的更友好，更适合开发者开发应用程序。
实现 MVVM
接下来使用上面的 Proxy 和 Reflect 来实现 MVVM，这里将 data 和 Proxy 输出到全局 Window 下，方便我们模拟数据双向联动的效果。

```html
<!DOCTYPE html>
<html>
  <div>name: <input id="name" /> age: <input id="age" /></div>
</html>
<script>
  // 与页面绑定
  const data = {
    name: '',
    age: 0,
  }

  // 暴露到外部，便于查看效果
  window.data = data
  window.myProxy = new Proxy(data, {
    set(target, propKey, value) {
      // 改变数据 Model 时修改页面
      if (propKey === 'name') {
        document.getElementById('name').value = value
      } else if (propKey === 'age') {
        document.getElementById('age').value = value
      }
      Reflect.set(...arguments)
    },
  })

  // 页面变化改变 Model 内数据
  document.getElementById('name').onchange = function (e) {
    Reflect.set(data, 'name', e.target.value)
  }
  document.getElementById('age').onchange = function (e) {
    Reflect.set(data, 'age', e.target.value)
  }
</script>
```

先打印了 data，然后模拟有异步数据过来，手动修改 data 里的数据 window.myProxy.age=25，这时候页面上的 age 联动变化为 25，再次打印了查看 data。接下来在页面上手动输入 name，输入完成后触发输入框的 onchange 事件后，再次查看 data，此时 model 里的数据已经变化为最新的与页面保持一致的值。
