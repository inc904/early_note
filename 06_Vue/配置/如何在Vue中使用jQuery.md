# 安装依赖

```
yarn add jquery
```

# 修改 build/webpack.base.conf.js

添加如下配置：

```javascript
var webpack = require('webpack')
```

在 `module.exports={}` 添加如下配置：

```javascript
//......表示省略已有的

module.exports = {
  // .....................
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      vue$: 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      jquery: 'jquery', //这里是增加的
    },
  },
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery',
      'windows.jQuery': 'jquery', //这里是增加的
    }),
  ],
  // .....................
}
```

# 在 main.js 中引入

```javascript
import $ from 'jquery'

import 'bootstrap/dist/css/bootstrap.min.css'
import 'bootstrap/dist/js/bootstrap.min.js'
```

# 在 Vue 组件中的 script 块中使用

```javascript
// 这是jq的代码

$(function(){
    $('.aui-content-main .aui-content-menu').hover(function(){
      $(this).addClass('active').find('s').hide();
      $(this).find('.aui-content-menu-dow').show();
    },function(){
      $(this).removeClass('active').find('s').show();
      $(this).find('.aui-content-menu-dow').hide();
    });
  });

// 这是vue的js代码
export default {...}
```

转载于:https://blog.51cto.com/xvjunjie/2399214
