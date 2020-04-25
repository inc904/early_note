## taro 路由及传参
### 路由
taro 的路由是自带的，不需要额外的配置，只需要在 App.js 下的 config 中配置 pages 即可。
```js
class App extends Component {
    config = {
        pages: [
            'pages/test/test',
            'pages/index/index'
        ],
    }
}
```
### taro 通过 api 跳转、替换

```js
import Taro from '@tarojs/taro'

// Taro.navigateTo(OBJECT)
// 使用方式同 wx.navigateTo, 支持 Promise 化使用。
Taro.navigateTo(params).then(...)

// Taro.redirectTo(OBJECT)
// 同 wx.redirectTo, 支持Promise
Taro.redirectTo(params).then(...)

// Taro.switchTab()

// Taro.navigateBack()

// Taro.relaunch()

// Taro.getCurrentPages()

```

### 路由传参

```js
Taro.navigateTo({
	url:'pages/page/index?id=2'
})
```
在跳转目标页面的生命周期方法(componentWillMount)中通过 `this.$router.params` 获取传入的参数。