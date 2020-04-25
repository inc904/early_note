

# JS合并两个数组：

```js
let a = [1,2,3]
let b = [4,5,6]
// 1. concat()
// concat 连接a,b之后，a，b两个数组的值不变，同时会返回一个新的数组。
// 这样在需要进行多次数组合并时，会造成很大的内存浪费。
let c = a.concat(b)


// 2. for 循环

for(var i in b){
    a.push(b[i])
}


// 3. apply


a.push.apply(a,b)
Array.prototype.push(a,b)
```
