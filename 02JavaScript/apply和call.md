# apply 和 call

1. 区别
2. 什么情况下选用
3. apply 的妙用

fn.call(obj,10,20,30)
fn.apply(obj,[10,20,30])

都是 function 原型的方法，改变 this 指向；
传参方法不同；

bind 也可以改变 this 指向，但是不立即执行函数，只是预先处理改变 this 指向。

性能：参数三个以上 call 的性能 好一些
三个以下，都一样

## apply:

方法能劫持另外一个对象的方法，继承另外一个对象的属性。

Fun.apply(obj,args) 方法能接收两个参数
obj: 这个对象代替 Function 类里的 this 对象
args： 这个是数组，它将作为参数传给 Fun (args --> arguments)

## call

call 和 apply 的 意思一样，只不过参数列表不一样
Fun.call(obj, [param1,[param2]])
obj: 这个对象代替 Fun 里的 this
params： 这是一个参数列表

## apply 示例

```js
function Person(name, age) {
  this.name = name
  this.age = age
}

function Student(name, age, grade) {
  // 用 this ==》 Student 代替 Person 内的 this，把形参 传给 Person， 继承 Person 内的 this.name = name
  Person.apply(this, arguments)

  // student 自己的属性
  this.grade = grade
}

var stu = new Student('zzc', 19, '一年级')
```

## call 示例

在 Student 函数里面可以将 apply 中修改

Person.call(this,name,age)

## 什么时候用

在给对象参数的情况下，如果参数形式是数组，比如 上面 Student 中 apply 传递了参数 arguments, 这个参数类型就是 数组类型，并且在调用 Person 的时候参数的列表是对应一致的(也就是 Person 和 Student 的参数列表前两位是一致的) 就可以采用 apply , 如果我的 Person 的参数列表是这样的(age,name),而 Student 的参数列表是(name,age,grade),这样就可以用 call 来实现了,也就是直接指定参数列表对应值的位置(Person.call(this,age,name,grade));

### 妙用

1. Math.max 可以实现得到数组中最大的一项
   Math.max(p1,p2,p3) 支持这样的形式
   可以：
   Math.max.apply(null, array)

2. 同理 Math.min 可以得到最小的一项
3. Array.prototype.push 实现两个数组的合并

push 方法没有提供 push 一个数组，提供了 push(p1,p2,p3)

```js
var a = [{ id: 1 }, { id: 2 }]
var b = [{ id: 3 }, { id: 4 }]

a.push.apply(a, b)
Array.prototype.push(a, b)
// 二者都可以实现，合并两个数组
```

> 一般在目标函数只需要 n 个参数列表,而不接收一个数组的形式（[param1[,param2[,…[,paramN]]]]）,可以通过 apply 的方式巧妙地解决这个问题!
