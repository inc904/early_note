```js
// 展开运算符用于数组或者对象
let arr = [1,2,3]
let arr2 = ['1',2,3,'a','n']
let obj = {a: 2, b: '3'}
let obj2 = {c: 3,d: 'aaaa'}
let obj3 = {a:"2",k:'123'}

let resArr = [...arr,...arr2]
let resObj1 = {...obj,...obj2}
let resObj2 = {...obj,...obj3}
console.log(resArr)
console.log(resObj1)
console.log(resObj2)
// 赋值操作 不会引起 展开后的 值的改变 
obj.a = 'hello'
console.log(obj)
console.log(resObj1)
```
在对象中赋值传递的是内存地址，在修改其中一个变量的时候会导致另一个变量发生改变，展开运算符就不会发生这样的情况，它直接将展开的值赋值给新的变量。