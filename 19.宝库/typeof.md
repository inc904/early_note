## typeof
一共六种返回类型值。返回值 为 字符串，且全为小写

```javascript
typeof 'hahah' // "string"
typeof true // "boolean"

typeof function(){} // "function"
typeof class c{} // "function"

typeof 123 // "number"
typeof NaN // "number"

typeof undefined // "undefined"


typeof [1,2] // "object"
typeof {"age": 12} // "object"
typeof null // "object"
````
对于 创建的 对象 ，他都会返回 `"object"`，所以如果要判断某个实例是否是某个对象的实例，则需要用到 `instanceof` 运算符

