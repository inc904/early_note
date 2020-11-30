## 数组循环

es5:

### forEach()

```js
/**
 * array.forEach(function (currentValue, index, arr){
	 // code
 }, thisValue)
 * 	currentValue： 当前元素
 * 	index： 当前元素的索引值
 *  arr：当前元素所属的数组
 * */

let arr = ['aa','bb','cc']
arr.forEach((value, index,arr) => {
	console.log(this+'===='+index+":"+value+" <= "+arr)
 //  由于是箭头函数形式 this指向是 当前作用域  window
},111)
// arr.forEach(function(val,index,arr){
//     console.log(this,val,index,arr);
//  // this 指向 Number(111)
// },111);


// 将数组中的每一项翻倍
arr.forEach(function(item,index,array){
    array[index] = item * 2;
});
console.log(arr);   // [2,-4,6,8,-10]
```

### map()

函数有返回值，如果不加返回值就跟 forEach() 一样，返回值是 undefined

```js
// Map()

// let result = arr.map((val, index,arr)=>{
// 	console.log(val, index, arr)
// })
// console.log(result)  // [undefined, undefined, undefined]
```

return 一个值：

```js
let arr = ['aaa','bbb','ccc'];
let newArr = arr.map((val,index,arr) => {
    console.log(val,index,arr);
    return 1;
    // "aaa" 0 ["aaa", "bbb", "ccc"]
    // "bbb" 1 ["bbb", "bbb", "ccc"]
    // "ccc" 2 ["ccc", "bbb", "ccc"]
    
});
console.log(newArr); // [1, 1, 1]
```

应用：

```js
let aNews = [
    {aaa: '为排行暴走万步', bbb: 404512},
    {aaa: '李荣浩庆生杨丞琳', bbb: 444512},
];
let newArr = aNews.map((val,index,arr) => {
    let json = {};
    json.title = `标题:${val.aaa}`;
    json.read = `阅览量:${val.bbb}`;
    return json;
});
console.log(newArr);
```





![img](https://upload-images.jianshu.io/upload_images/8560482-185dd555148b270d.png?imageMogr2/auto-orient/strip|imageView2/2/w/547/format/webp)

### filter()

用来过滤一些不合格的元素，如果回调函数返回的是true，那么自然会被留下来，为false的就会被过滤掉

```js
let aNews = [
    {title: '为排行暴走万步', read: 404512, hot: false},
    {title: '李荣浩庆生杨丞琳', read: 444512, hot: true},
];
let newArr = aNews.filter((val,index,arr) => {
    return val.hot==true;
});
console.log(newArr);
```

![img](https://upload-images.jianshu.io/upload_images/8560482-a3abf59436660fd2.png?imageMogr2/auto-orient/strip|imageView2/2/w/473/format/webp)

### some()

```js
let aNews = ['aaa','bbb','ccc'];
let result = aNews.some((item,index,arr) => {
    return item=='aaa';
});
console.log(result);  // true
```

### every()

和some一样，只不过是查找数组中的每一项，所有元素都要符合条件，才返回true：

```js
let arr = [1,3,5,7,9];
let result = arr.every((val,index,arr)=>{
    return val%2==1;  // 判断是不是奇数
});
console.log(result);  // true
```



① forEach()无返回值，map()和filter()返回新数组，every()和some()返回布尔值
 ② 匿名函数中this指向默认为window，可通过传第二参数来更改之
 ③ 五种遍历方法均为ES5方法

 以上五大方法除了传递一个匿名函数作为参数之外，还可以传第二个参数，该参数用于指定匿名函数内的this指向





### reduce()和reduceRight()

- reduce():从左往右运算→

  ```js
  arr.reduce(function(prev,cur,index,arr){
  ...
  }, init);
  arr 表示原数组；
  prev 表示上一次调用回调时的返回值，或者初始值 init;
  cur 表示当前正在处理的数组元素；
  index 表示当前正在处理的数组元素的索引，若提供 init 值，则索引为0，否则索引为1；
  init 表示初始值。
  
  ```

  #### 数组去重

  ```js
  var newArr = arr.reduce(function (prev, cur) {
      prev.indexOf(cur) === -1 && prev.push(cur);
      return prev;
  },[]);
  ```

  #### 求最大项：

  ```js
  var max = arr.reduce(function (prev, cur) {
      return Math.max(prev,cur);
  });
  ```

  

- reduceRight()从右往左运算←

可以用来数组的求和，阶乘，幂运算；接收四个参数

```js

let arr = [2,3,3];
let result = arr.reduce((prev,curr,index,arr)=>{
    return prev-curr;   // 运算的方式
});
console.log(result);  // -4

```

```js
let arr = [2,3,3];
let newArr = arr.reduceRight((prev,curr,index,arr)=>{
    return prev-curr;   // 运算的方式
});
console.log(newArr);  // -2
```





- ES2017新增的幂运算符`**`

```js
let arr = [2,3,2];
let newArr = arr.reduce((prev,curr,index,arr)=>{
    return Math.pow(prev,curr);
        //return prev**curr;
});
console.log(newArr);    // 64
```



es6:

### for...of...

```js
let arr = ['aaa','bbb','ccc'];
for (let val of arr) {
    console.log(val);   // 输出每一项
    // aaa
    // bbb
    // ccc
}

for (let index of arr.keys()) {
    console.log(index); // 输出每一项的索引
    // 0
    // 1
    // 2
}

for (let item of arr.entries()) {
    console.log(item);  // 输出三个数组
    // [0, "aaa"]
    // [1, "bbb"]
    // [2, "ccc"]
    console.log(item[0]);   // 0 1 2
    console.log(item[1]);   // aaa bbb ccc
}

for (let [key,val] of arr.entries()) {
    console.log(key,val);   
    // 0 "aaa"
    // 1 "bbb"
    // 2 "ccc"
}
```

