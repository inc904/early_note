## 类的由来

```js
function Point(x, y) {
  this.x = x
  this.y = y
}
Point.prototype.toString = function () {
  return '(' + this.x + '---->' + this.y + ')'
}
var p = new Point(2, 3)
console.log(p.toString())

// es6 的类 完全可以看作构造函数的另一种写法
class Point1 {
  constructor(x, y) {
    // 构造方法
    // this 关键字 代表 实例对象
    this.x = x
    this.y = y
  }
  toString() {
    return '(' + this.x + '---->' + this.y + ')'
  }
}
var p1 = new Point1('a', 'b')
console.log(p1.toString())
console.log(typeof Point) // function
console.log(Point === Point.prototype.constructor) // true
// 上述代码表明，类的数据类型就是函数，类本身就指向构造函数。
/**
 * 构造函数的 prototype 属性，在 ES6 的类上继续存在。
 * 事实上，类的所有方法都定义在类的 prototype 属性上面
 */
class Point {
  constructor() {}
  toString() {}
  toValue() {}
}
// 等价于
// constructor() toString() toValue() 都定义在 Point.prototy上面
Point.prototype = {
  constructor() {},
  toString() {},
  toValue() {},
}
// 因此，在类的实例上面调用方法，其实就是在调用原型上的方法
class B {}
const b = new B()
b.constructor === B.prototype.constructor // true

// 上面 b是B类的实例，他的 constructor() 方法就是B原型的 constructo()方法

// 由于类的方法都定义在 “prototype” 对象上面，所以类的新方法可以添加在 prototype 对象上。 Object.assign() 方法可以一次向类添加多个方法

class Point {
  constructor() {}
}
Object.assign(Point.prototype, {
  toString() {},
  toValue() {},
})

// prototype 对象的 constructor() 属性，直接指向 类 本身，这与 ES5 报纸一致

Point.prototype.constructor === Point // true

// 类的内部 所有定义的方法，都是不可枚举的（non-enumerable）,这与 ES5 的行为不一致

class Point {
  constructor() {}
  toString() {}
}
Object.keys(Point.prototype) // []
Object.getOwnPropertyNames(Point.prototype) // ["constructor", "toString"]

// 采用 ES5 的写法， toString方法就是可枚举的

var Point = function (x, y) {}
Point.prototype.toString = function () {}
Object.keys(Point.prototype) // ["toString"]
Object.getOwnPropertyNames(Point.prototype) // ["constructor", "toString"]

```

## constructor

`constructor`是类的默认方法，通过`new`命令生成对象实例时，自动调用该该方法。一个类必须又`constructor()`,没有显式定义，一个空的`constructor()`会被默认添加。

类必须使用`new`调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用`new`也可以执行。

## 类的实例

与 ES5 一样，实例的属性除非显式定义在其本身（即定义在`this`对象上），否则都是定义在原型上（即定义在`class`上）。

```js
//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```

上面代码中，`x`和`y`都是实例对象`point`自身的属性（因为定义在`this`变量上），所以`hasOwnProperty()`方法返回`true`，而`toString()`是原型对象的属性（因为定义在`Point`类上），所以`hasOwnProperty()`方法返回`false`。这些都与 ES5 的行为保持一致。

与 ES5 一样，类的所有实例共享一个原型对象。

```javascript
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__ === p2.__proto__
//true
```

上面代码中，`p1`和`p2`都是`Point`的实例，它们的原型都是`Point.prototype`，所以`__proto__`属性是相等的。

这也意味着，可以通过实例的`__proto__`属性为“类”添加方法。

`__proto__` 并不是语言本身的特性，这是各大厂商具体实现时添加的私有属性，虽然目前很多现代浏览器的 JS 引擎中都提供了这个私有属性，但依旧不建议在生产中使用该属性，避免对环境产生依赖。生产环境中，我们可以使用 `Object.getPrototypeOf` 方法来获取实例对象的原型，然后再来为原型添加方法/属性。

```javascript
var p1 = new Point(2,3);
var p2 = new Point(3,2);

p1.__proto__.printName = function () { return 'Oops' };

p1.printName() // "Oops"
p2.printName() // "Oops"

var p3 = new Point(4,2);
p3.printName() // "Oops"
```

上面代码在`p1`的原型上添加了一个`printName()`方法，由于`p1`的原型就是`p2`的原型，因此`p2`也可以调用这个方法。而且，此后新建的实例`p3`也可以调用这个方法。这意味着，使用实例的`__proto__`属性改写原型，必须相当谨慎，不推荐使用，因为这会改变“类”的原始定义，影响到所有实例。

## getter&setter

### TODO

与 ES5 一样，在“类”的内部可以使用`get`和`set`关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。

```javascript
class MyClass {
  constructor() {
    // ...
  }
  get prop() {
    return 'getter';
  }
  set prop(value) {
    console.log('setter: '+value);
  }
}

let inst = new MyClass();

inst.prop = 123;
// setter: 123

inst.prop
// 'getter'
```

### 属性表达式

类的属性名，可以采用表达式。

```javascript
let methodName = 'getArea';

class Square {
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```

上面代码中，`Square`类的方法名`getArea`，是从表达式得到的。

## class 表达式

```javascript
const Myclass= class Me{
    getClassName(){
        retunr Me.name
    }
}
```

上面代码使用表达式定义了一个类。需要注意的是，这个类的名字是`Me`，但是`Me`只在 Class 的内部可用，指代当前类。在 Class 外部，这个类只能用`MyClass`引用。

```javascript
let inst = new MyClass();
inst.getClassName() // Me
Me.name // ReferenceError: Me is not defined
```

上面代码表示，`Me`只在 Class 内部有定义。

如果类的内部没用到的话，可以省略`Me`，也就是可以写成下面的形式。

```javascript
const MyClass = class { /* ... */ };
```

采用 Class 表达式，可以写出立即执行的 Class。

```javascript
let person = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}('张三');

person.sayName(); // "张三"
```

上面代码中，`person`是一个立即执行的类的实例。

## 静态方法

类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用，这就称为“静态方法”。

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

Foo.classMethod() // 'hello'

var foo = new Foo();
foo.classMethod()
// TypeError: foo.classMethod is not a function
```

上面代码中，`Foo`类的`classMethod`方法前有`static`关键字，表明该方法是一个静态方法，可以直接在`Foo`类上调用（`Foo.classMethod()`），而不是在`Foo`类的实例上调用。如果在实例上调用静态方法，会抛出一个错误，表示不存在该方法。

注意，如果静态方法包含`this`关键字，这个`this`指的是类，而不是实例。

```javascript
class Foo {
  static bar() {
    this.baz();
  }
  static baz() {
    console.log('hello');
  }
  baz() {
    console.log('world');
  }
}

Foo.bar() // hello
```

上面代码中，静态方法`bar`调用了`this.baz`，这里的`this`指的是`Foo`类，而不是`Foo`的实例，等同于调用`Foo.baz`。另外，从这个例子还可以看出，静态方法可以与非静态方法重名。

父类的静态方法，可以被子类继承。

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
}

Bar.classMethod() // 'hello'
```

上面代码中，父类`Foo`有一个静态方法，子类`Bar`可以调用这个方法。

静态方法也是可以从`super`对象上调用的。

```javascript
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
  static classMethod() {
    return super.classMethod() + ', too';
  }
}

Bar.classMethod() // "hello, too"
```

## 实例属性的写法

实例属性除了定义在`constructor()`方法里面的`this`上面，也可以定义在类的最顶层

```js
class IncreasingCounter{
    constructor(){
        this._count = 10
    }
    get value(){
        console.log('Getting the current value')
        return this._count
    }
    increment(){
        this._count++
    }
}
```

上面代码中，实例属性`this._count`定义在`constructor()`方法里面。另一种写法是，这个属性也可以定义在类的最顶层，其他都不变。

```js
class IncreasingCounter {
    _count = 10
	get value(){
        console.log('Getting the current value')
        return this._count
    }
	increment(){
        this._count++
    }
}
```

上面代码中，实例属性`_count`与取值函数`value()`和`increment()`方法，处于同一个层级。这时，不需要在实例属性前面加上`this`。

上面代码中，实例属性`_count`与取值函数`value()`和`increment()`方法，处于同一个层级。这时，不需要在实例属性前面加上`this`。

这种新写法的好处是，所有实例对象自身的属性都定义在类的头部，看上去比较整齐，一眼就能看出这个类有哪些实例属性。

```javascript
class foo {
  bar = 'hello';
  baz = 'world';

  constructor() {
    // ...
  }
}
```

上面的代码，一眼就能看出，`foo`类有两个实例属性，一目了然。另外，写起来也比较简洁。

## 静态属性

静态属性指的是 Class 本身的属性，即`Class.propName`,而不是定义在实例对象`this`上的属性。

```js
class Foo{ }
Foo.prop = 1 
console.log(Foo.prop) // 1
```

上面的写法为`Foo`类定义了一个静态属性`prop`

目前只有这种方法可行。因为ES6 明确规定，`Class 内部只有静态方法，没有静态属性`。现在有一个提案提供了类的静态属性，写法是在实例属性的前面，加上`static` 关键字。

```js
class MyClass {
    static myStaticProp = 42
	constructor (){
        console.log(MyClass.myStaticProp)
    }
}
```

这个新写法大大方便了静态属性的表达。

```javascript
// 老写法
class Foo {
  // ...
}
Foo.prop = 1;

// 新写法
class Foo {
  static prop = 1;
}
```

上面代码中，老写法的静态属性定义在类的外部。整个类生成以后，再生成静态属性。这样让人很容易忽略这个静态属性，也不符合相关代码应该放在一起的代码组织原则。另外，新写法是显式声明（declarative），而不是赋值处理，语义更好。

## 私有方法和私有属性

## `new.target` 属性