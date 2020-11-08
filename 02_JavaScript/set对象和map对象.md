## set 对象

set 本身是一个函数，用来构建对象，即构造函数，对象的实例化。

```js
let arr = [1, 1 , 2, 3, 4, 5]
let s = new Set(arr)
console.log(s) // s = [1, 2, 3, 4, 5]

# 会自动去重

## set 的属性和方法
s.size() // 相当于 length
s.clear() // 清空所有值
s.delete(4) // 删掉 4 返回布尔值
s.get() //
s.has() // 查看是否包含 返回 布尔值
s.add(6) // 添加一项
```

## map 对象
