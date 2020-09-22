# [彻底搞懂路由跳转：location 和 history 接口](https://segmentfault.com/a/1190000014120456)

单页面应用中，路由由前端配置，根据不同URL显示不同的内容。

原理要明白浏览器提供的两种API：

1. window.location
   - location.href
   - location.hash
   - location.search
   - location.pathname
2. window.history
   - history.pushState()
   - history.replaceState()
   - history.go()
   - history.back()
   - history.forward()



# window.location

我们先了解 location 对象，location 有很多的属性。我们可以通过改变其属性值修改页面的 url。我们在单页应用中需要做到的是改变 url 不刷新页面，location 接口提供以下两种方式可以做到：

1. `location.href` 赋值时只改变 url 的 hash
   ![图片描述](https://segmentfault.com/img/bV7pcG?w=968&h=378)
2. 直接赋值 `location.hash`
   ![图片描述](https://segmentfault.com/img/bV7pc1?w=944&h=440)

而上面的列出其余两个属性 `location.search` 会直接刷新页面，这个就不解释了。但 `location.pathname` 照道理来说只改变 hash 应该是可以的，但实际上浏览器会编码这个属性值，所以无法直接赋带 # 号的值。



在实际应用的时候，重新刷新页面的时候，我们通常使用： location.reload() 或者是 history.go(0) 来做。因为这种做法就像是客户端点F5刷新页面，所以页面的method="post"的时候，会出现“网页过期”的提示。那是因为Session的安全保护机制。

可以想到：当调用 location.reload() 方法的时候，页面此时在服务端内存里已经存在， 因此必定是IsPostback 的。

  如果有这种应用：我们需要重新加载该页面，也就是说我们期望页面能够在服务端重新被创建，我们期望是 Not IsPostback 的。这事，location.replace() 就可以完成此任务。被replace的页面每次都在服务端重新生成。可以这么写：location.replace(location.href)

而重定向则用herf 和replace 

1、location.href='http://www.xxx.com/';

2、location.replace('http://www.xxx.com/');

**两者的不同之处是前者会在浏览器的历史浏览记录（history对象中增加一条新的记录，而后者则是相当于用replace中的url代替了现有的页面url，并把history中的url也替换为重定向后的url。**

# window.history

[history 接口](https://developer.mozilla.org/zh-CN/docs/Web/API/History)是 HTML5 新增的，它有五个方法可以改变 url 而不刷新页面。

1. `history.pushState()`
   ![图片描述](https://segmentfault.com/img/bV7pg8?w=936&h=434)
2. `history.replaceState()`
   ![图片描述](https://segmentfault.com/img/bV7phf?w=950&h=478)
3. `history.go()`
   ![图片描述](https://segmentfault.com/img/bV7phg?w=854&h=578)

上面只演示了三个方法，因为 `history.back()` 等价于 `history.go(-1)`，`history.forward()` 则等价于 `history.go(1)`，这三个接口等同于浏览器界面的前进后退。

# 如何监听 url 的变化

现在我们已经知道如何不刷新页面改变页面的 url。虽然页面没刷新，但我们要改变页面显示的内容。这就需要 js 监听 url 的变化从而达到我们的目的。

我们有两个事件可以监听 url 的改变：

## hashchange

`hashchange` 事件能监听 url hash 的改变。

先要加上事件监听的代码：

```
window.addEventListener('hashchange', function(e) {
  console.log(e)
})
```

然后就可以在页面的 console 里愉快的实验了：

![图片描述](https://segmentfault.com/img/bV7plH?w=970&h=974)

从上图中我们可以知道不管是通过 location 接口直接改变 hash，还是通过 history 接口前进后退（只是 hash 改变的情况下），我们都可以监听到 url hash 的改变。但这个事件也只能监听 url hash 的变化。所以我们需要一个更强大的事件：`popstate`。

## popstate

[popstate](https://developer.mozilla.org/zh-CN/docs/Web/Events/popstate) 事件能监听除 `history.pushState()` 和 `history.replaceState()` 外 url 的变化。

先加上事件监听的代码：

```
window.addEventListener('popstate', function(e) {
  console.log(e)
})
```

然后又可以在页面的 console 里愉快的实验了：

![图片描述](https://segmentfault.com/img/bV7pow?w=970&h=750)

其实不止 `history.pushState()` 和 `history.replaceState()` 对 url 的改变不会触发 `popstate` 事件，当这两个方法只改变 url hash 时也不会触发 `hashchange` 事件。

# hash 模式和 history 模式

我们都知道单页应用的路由有两种模式：hash 和 history。如果我们在 hash 模式时不使用 `history.pushState()` 和 `history.replaceState()` 方法，我们就只需要在 `hashchange` 事件回调里编写 url 改变时的逻辑就行了。而 history 模式下，我们不仅要在 `popstate` 事件回调里处理 url 的变化，还需要分别在 `history.pushState()` 和 `history.replaceState()` 方法里处理 url 的变化。而且 history 模式还需要后端的配合，不然用户刷新页面就只有 404 可以看了?

所以 hash 模式下我们的工作其实是更简单的，但为什么现在都推荐用 history 模式呢？总不是 hash 模式下的 url 太丑了，毕竟这是个看脸的世界?

不过 `vue-router` 在浏览器支持 `pushState()` 时就算是 hash 模式下也是用 `history.pushState()` 来改变 url，不知道有没什么深意？还有待研究...