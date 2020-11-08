移动端：rem + flex 

## 一、在js中统一计算配置

核心代码：

### 代码一：
```js
export default function() {
    // var devicePixelRatio = 1;
    // var scale = 1 / devicePixelRatio;
    // document.querySelector('meta[name="viewport"]').setAttribute('content','initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
    // 7.5根据设计稿的横向分辨率/100得来
    // alert(document.documentElement.clientWidth)
    var deviceWidth = document.documentElement.clientWidth;
    // var deviceWidth = window.screen.availWidth
    // alert(navigator.userAgent)
    // alert(deviceWidth)
    // console.log(navigator.userAgent)
    if(deviceWidth > 750) {
        // deviceWidth = 750;
        deviceWidth = 7.5 * 50;
    }

    document.documentElement.style.fontSize = deviceWidth / 7.5 + 'px';

    // 禁止双击放大
    document.documentElement.addEventListener('touchstart', function (event) {
        if (event.touches.length > 1) {
            event.preventDefault();
        }
    }, false);
    var lastTouchEnd = 0;
    document.documentElement.addEventListener('touchend', function (event) {
        var now = Date.now();
        if (now - lastTouchEnd <= 300) {
            event.preventDefault();
        }
        lastTouchEnd = now;
    }, false);
}
```
### 代码二：

```js
// rem等比适配配置文件
// 基准大小
const baseSize = 16
// 设置 rem 函数
function setRem () {
  // 当前页面宽度相对于 1920宽的缩放比例，可根据自己需要修改。
  const scale = document.documentElement.clientWidth / 1920
  // 设置页面根节点字体大小（“Math.min(scale, 2)” 指最高放大比例为2，可根据实际业务需求调整）
  document.documentElement.style.fontSize = baseSize * Math.min(scale, 2) + 'px'
}
// 初始化
setRem()
// 改变窗口大小时重新设置 rem
window.onresize = function () {
  setRem()
}
```

### 代码三
```js
fnResize();
window.onresize = function () {
  fnResize();
}
function fnResize() {
  var deviceWidth = document.documentElement.clientWidth || window.innerWidth;
  if (deviceWidth >= 750) {
    deviceWidth = 750;
  }
  if (deviceWidth <= 320) {
    deviceWidth = 320;
  }
  document.documentElement.style.fontSize = (deviceWidth / 7.5) + 'px';
}
```

将代码在 main.js或index.html 中引用。在样式中使用 rem 单位。

## 二、借助 px2rem-loader 插件
- 安装
安装 `px2rem-loader` 、`lib-flexible` 或者 `px2rem-loader` 、`amfe-flexible`
```bash
npm install px2rem-loader lib-flexible --save
```
- 在项目入口文件main.js中 引入 lib-flexible
```js
import 'lib-flexible/flexible.js'
```
- 在 bulid 下的 utils.js 中找到 generateLoaders，添加
```js
const cssLoader = {
	loader: cssLoader,
	options:{
		minimize: process.env.NODE_ENV  === 'production',
		sourceMap: options.sourceMap,
		importLoaders: 2 // 在 css-loader 前应用的 loader 的数目，默认为 0 ，
		//  如果不加这个，@import 的外部 css 文件 不能正常转换
	}
}
const px2remLoader = {
	loader: 'px2rem-loader',
	options:{
		remUnit: 7.5 // 设计稿的 1/10
	}
}

function generateLoaders (loader, loaderOption){
	// const loaders = [cssLoader, px2remLoader]
	const loaders = options.usePossCSS ? [cssLoader, possLoader, px2remLoader]: [cssLoader, px2remLoader]

	if(loader){
		loaders.push({
			loader: loader + '-loader',
			options: Object.assign({}, loaderOption, {
				sourceMap: options.sourceMap
			})
		})
	}
}
```

- 重启项目，px被转化为 rem 了。

另外，px 写法上会有些不同，大家可以参考 px2rem 官方介绍，下面简单介绍一下。

1. 直接写 px，编译后会直接转化成 rem；---- 【除下面两种情况，其他长度用这个】

2. 在 px 后面添加 /*no*/，不会转化 px，会原样输出； ---- 【一般 border 用这个】

3. 在 px 后面添加 /*px*/，会根据 dpr 的不同，生成三套代码。---- 【一般 font-size 用这个】



以上实现转换适用于：

（1）组件中编写的<style></style>下的css

（2）从index.js或者main.js中import ‘../../static/css/reset.css’引入css

（3）在组件的<script type=”text/ecmascript-6″> import ‘../../static/css/reset.css'</script>中引入css

另外的情况不适用：

（1）组件<style></style>中@import “../../static/css/reset.css (可考虑上面（2）、（3）的形式引入)

（2）外部样式:<link rel=”stylesheet” href=”static/css/reset.css”>

（3）元素内部样式：style=”height: 417px; width: 550px;”

### 三

第一步，安装 postcss-px2rem及px2rem-loader

打开命令行工具，输入以下指令安装插件(当然用淘宝镜像cnpm安装会更快)

```bash
npm install postcss-px2rem px2rem-loader --save
```

第二步，在根目录src中新建util目录下新建rem.js等比适配文件
```js
// rem等比适配配置文件
// 基准大小
const baseSize = 16
// 设置 rem 函数
function setRem () {
  // 当前页面宽度相对于 1920宽的缩放比例，可根据自己需要修改。
  const scale = document.documentElement.clientWidth / 1920
  // 设置页面根节点字体大小（“Math.min(scale, 2)” 指最高放大比例为2，可根据实际业务需求调整）
  document.documentElement.style.fontSize = baseSize * Math.min(scale, 2) + 'px'
}
// 初始化
setRem()
// 改变窗口大小时重新设置 rem
window.onresize = function () {
  setRem()
}
```
第三步，在main.js中引入适配文件

```bash
import './util/rem'
```

第四步，到vue.config.js中配置插件
```js
// 引入等比适配插件
const px2rem = require('postcss-px2rem')

// 配置基本大小
const postcss = px2rem({
  // 基准大小 baseSize，需要和rem.js中相同
  remUnit: 16
})

// 使用等比适配插件
module.exports = {
  lintOnSave: true,
  css: {
    loaderOptions: {
      postcss: {
        plugins: [
          postcss
        ]
      }
    }
  }
}

```
### 3.2
在使用vue-cli搭建好项目框架后,在目录结构的index.html文件中添加一段js代码:
```js
fnResize();
window.onresize = function () {
  fnResize();
}
function fnResize() {
  var deviceWidth = document.documentElement.clientWidth || window.innerWidth;
  if (deviceWidth >= 750) {
    deviceWidth = 750;
  }
  if (deviceWidth <= 320) {
    deviceWidth = 320;
  }
  document.documentElement.style.fontSize = (deviceWidth / 7.5) + 'px';
}
```
然后在写css就可以将px单位换成rem.

这里设置的比例是100px=1rem,

例如:宽度为100px时,可以直接写成1rem

=============================================================
### 3.3

2==vue cli3.0 rem 使用
vue cli3.0 rem 使用
首先安装amfe-flexible插件，在main.js里引入

1、`npm i amfe-flexible`

2、`import 'amfe-flexible'`

然后再，安装postcss-px2rem插件 `npm i postcss-px2rem`

在package.json中配置

```json
"postcss": {
    "plugins": {
      "autoprefixer": {},
      "postcss-px2rem": {
        "remUnit": 37.5
      }
    }
  }

```
.
说明，我这里用的是vue-cli3.0脚手架。在.vue文件里。样式直接写px单位就可以了。在浏览器查看时会自动转换为rem单位。如果字体还想用px。那就这样将px大写。就不会编译为rem单位了。样式就可以实现px。


## 参考链接

- [vue移动端适配](https://www.jianshu.com/p/84169b420ff5)
- [vue-cli 配置flexible](https://segmentfault.com/a/1190000011883121)
- [vue中使用第三方UI库的移动端rem适配方案](https://segmentfault.com/a/1190000015238394)
- [手机端vue+vant+rem项目适配750px设计稿的配置](https://www.jianshu.com/p/eb811a33ad63)
- [vue 中使用 rem 布局的两种方法](https://www.pianshen.com/article/6624190736/)
- [基于vue-cli配置手淘的lib-flexible + rem，实现移动端自适应](https://segmentfault.com/a/1190000011883121)
- [vue中rem的配置](https://www.jianshu.com/p/7e98f9c44c97)
- [vue 中使用rem布局](https://www.cnblogs.com/xiaoxiaoxun/p/11147097.html)