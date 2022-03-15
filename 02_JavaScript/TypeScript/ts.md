## 类类型

### ES6 中类用法

#### 属性和方法

使用`class`定义类,使用`constructor`定义构造函数。

```js
class Animal {
  public name
  constructor(name) {
    this.name = name
  }
  sayHi(){
    return `My name is  ${this.name}.`
  }
}

let a = new Animal('Jerry')
console.log(a.sayHi()) // My name is Jerry.
```

#### 类的继承

使用`extends`关键字实现继承，子类中使用`super`关键字调用父类的构造函数和方法。

```js
class Cat extends Animal {
  constructor(name) {
    super(name)
    console.log(this.name)
  }
  sayHi() {
    return 'Meow,' + super.sayHi() // 调用父类的sayHi()
  }
}
let c = new Cat('Tom')
console.log(c.sayHi())
```

### 类类型

```ts
interface ClockInterface {
  curretnTime: Date
}

class Clock implements ClockInterface {
  curretnTime: Date
  constructor(h: number, m: number) {}

  setTime(d: Date) {
    this.curretnTime = d
  }
}
```

```ts
interface ClockInterface {
  tick()
}

interface ClockConstructor {
  new (hour: number, minute: number): ClockInterface
}
function createClock(
  ctor: ClockConstructor,
  hour: number,
  minute: number
): ClockInterface {
  return new ctor(hour, minute)
}

class DigitalClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log('beep beep')
  }
}

class AnalogClock implements ClockInterface {
  constructor(h: number, m: number) {}
  tick() {
    console.log('tick toc')
  }
}
let digital = createClock(DigitalClock, 12, 12)
let analog = createClock(AnalogClock, 12, 12)
```

## 继承接口

```javaScript
interface Shape {
  color: string;
}
interface PenStrock {
  penWidth: number;
}
interface Squre extends Shape, PenStrock {
  sideLigth: number;
}
// let squre1: Squre = {} // 缺少类型
let squre = {} as Squre; // 类型断言
squre.color = "cyan";
squre.sideLigth = 10;
squre.penWidth = 6;
```

## 混合类型

```ts
interface Counter {
  (start: number): string
  interval: number
  reset(): void
}
function getCounter(): Counter {
  let counter = function (start: number) {} as Counter
  counter.interval = 123
  counter.reset = function () {}
  return counter
}

let c = getCounter()
c(10)
c.reset()
c.interval = 5.0
```

## 接口继承类

```ts
class Control {
  private state: any
}
interface SelectorContaol extends Control {
  select()
}
class Button extends Control implements SelectorContaol {
  select() {}
}
class TextBox extends Control {
  select() {}
}
// 报错 没有继承类 就没有state
class ImageC implements SelectorContaol {
  select() {}
}
```

## 基本示例-->继承
