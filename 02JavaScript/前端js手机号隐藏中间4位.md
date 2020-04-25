一、

```js
var str='13888888888';  
var str2 = str.substr(0,3)+"****"+str.substr(7);  
console.log(str2);
```

 

二、

```js
var str = '13888888888';  
var str2 = str.replace(/(\d{3})\d{4}(\d{4})/, '$1****$2');
console.log(str2);
```

 

