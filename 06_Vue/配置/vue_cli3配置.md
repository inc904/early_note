## 项目配置：
- 别名配置 

```js
// vue.config.js
const path = require('path')
function resolve(dir){
	return path.join(__dirname, dir)
}

module.export = {
	chainWebpack: config => {
		config.resolve.alias
		// 配置别名
			.set('@', resolve('src'))
	}
}
```