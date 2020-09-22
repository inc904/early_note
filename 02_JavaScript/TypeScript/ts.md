#### 类类型

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

#### 继承接口

```ts
interface Shape {
  color: string
}
interface PenStrock {
  penWidth: number
}
interface Squre extends Shape, PenStrock {
  sideLigth: number
}
// let squre1: Squre = {} // 缺少类型
let squre = {} as Squre // 类型断言
squre.color = 'cyan'
squre.sideLigth = 10
squre.penWidth = 6
```

#### 混合类型

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

#### 接口继承类

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

#### 基本示例-->继承
