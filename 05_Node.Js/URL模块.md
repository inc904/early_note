### url模块
```js
const url = require('url')
url.parse('https://www.bilibili.com/video/av27670326/?p=34', true)
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'www.bilibili.com',
  port: null,
  hostname: 'www.bilibili.com',
  hash: null,
  search: '?p=34',
  query: [Object: null prototype] { p: '34' },
  pathname: '/video/av27670326/', 
  path: '/video/av27670326/?p=34',
  href: 'https://www.bilibili.com/video/av27670326/?p=34'
}
```