# axios报错： Cannot read property 'protocol' of undefined

错误：

```js
Uncaught (in promise) TypeError: **Cannot read property 'protocol' of undefined ...
```

源码：

完整错误：

```js
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(axios, VueAxios)
```

修正一：（亲测）

```js
import axios from 'axios'
import VueAxios from 'vue-axios'
Vue.use(VueAxios, axios) // 交换位置
```

修正二:

```js
import axios from 'axios'
//Vue.use(axios) // 不用这个
Vue.prototype.$http = axios // 挂载到原型
```

