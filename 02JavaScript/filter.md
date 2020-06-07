# filter

### 数组保留奇数
```js
var arr = [1,2,3,4,5,6,7]
var r = arr.filter(item => {
	return x % 2 !== 0
} )

r: [1,3,5,7]
```


### 数组 去除空格

```js
var arr = ['A','','B', null, undefined,'C',' ']
var r = arr.filter(s => return item && item.trim() )

r:['A', 'B', 'C']

```

## 回调函数

filter 接收的回到函数，其实可以有多个参数，通常我们仅使用第一个参数，表示Array 的某个参数，回调函数还可以接收 另外两个参数，表示元素的位置和数组本身。
```js
var arr = ['A'.'B','C']
var r = ar.filter(function(element, index, self){
	console.log(element) // 依次打印 'A','B','C'
	console.log(index) // 依次打印0，1，2
	console.log(self) // self就是数组本身
	return true
})
```

### 利用数组去重
```js
var r ,
		arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];

r = arr.filter((item, index, self)=>{
	return self.indexOf(item) === index
})


```