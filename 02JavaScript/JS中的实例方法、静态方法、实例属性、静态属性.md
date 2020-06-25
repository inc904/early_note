### 静态方法：

```js
function A() {}
A.color = 'red' // 静态属性
A.say = function () {
  console.log('hello')
} // 静态方法
A.say() // 输出‘hello’
```

静态方法：构造函数本身上添加的成员 ；构造函数的静态方法，不能通过实例调用

### 实例方法

```js
function A() {
  this.Color = 'blue' // 实例属性
}
A.prototype.age = 14 // 实例属性
A.prototype.run = function () {
  console.log('run')
} // 实例方法
var a = new A()
a.say() //
```

构造函数中 this 上添加的成员 ,在 A 构造方法里面，定义在 this 中的变量和方法，只有实例才能访问到：如 this.name,this.move,this.eat 这些都是实例拥有，无法通过 A 直接调用。

实例方法就是只有实例可以调用，静态方法只有构造函数可以调用
