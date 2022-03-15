# TS 基础

[typescript-tutorial](https://github.com/joye61/typescript-tutorial)

[typescript 中文文档](https://www.tslang.cn/docs/handbook/basic-types.html)

[typescript 入门教程](https://ts.xcatliu.com/)

[TypeScript](https://www.typescriptlang.org/)

## 写在前面

JavaScript 强制类型的最好理由：他可以 **让绝大部分错误发生在编码阶段，而不是让错误发生在线上**。

### 什么是值：

凡是可以被变量存储的单元都是值。它可以是简单的字符串、数字，也可以是复杂的由多条语句组成的代码单元，如类、函数、对象等：

```tsx
// 字符串作为值
let stringValue = "hello world";

// 对象字面量作为值
let objectLiteraValue = {
  attribute: "hello world",
};
// 函数作为值
let funValue = function () {};

// 函数作为返回值
function fn() {
  return "hello world";
}
let returnValue = fn();

// 类作为值
let classValue = class {};
```

在 Typescript 中，所有的值都具有 **强制类型**，值的类型化是 Typescript 区别于 JavaScript 最显著的特征。

> 实际上，JavaScript 也是有类型的，只不过 JavaScript 的类型信息是在编译阶段由编译器判定，对程序员来说，值是可以任意赋予的，编写代码时，就好像类型弱的不存在一样。

## 一、类型

### 1.1 值的类型化

#### 类型注解

类型注解是指在源代码中 **显式指定值的类型**，格式：**冒号+类型**

```js
// 字符串类型
let str: string = "hello world";

// 指定类的属性类型
class Hello {
  show: boolean = true;
}

// 指定函数参数和返回值类型
function sum(a: number, b: number) {
  return a + b;
}
```

下表列举了 TypeScript 支持的所有类型

| 类型           | 语法形式                           |
| -------------- | ---------------------------------- | --- | ---- |
| 数字类型       | `number`                           |
| 布尔类型       | `boolean`                          |
| 字符串类型     | `string`                           |
| 符号类型       | `symbol`                           |
| Void 类型      | `void`                             |
| Null 类型      | `null`                             |
| Undefined 类型 | `undefined`                        |
| Never 类型     | `never`                            |
| 任意类型       | `any`                              |
| 数组类型       | `T[]`                              |
| 元组类型       | `[T0, T1, ...]`                    |
| 枚举类型       | `enum T { ... }`                   |
| 函数类型       | `(p1: T1, p2: T2, ...) => T`       |
| 类类型         | `T`                                |
| 构造器类型     | `new (p1: T1, p2: T2, ...) => R`   |
| 对象类型       | `{ ... }` 或 `interface T { ... }` |
| 联合类型       | `T1                                | T2  | ...` |
| 交叉类型       | `T1 & T2 & ...`                    |

#### 类型推导

日常开发中，类型注解是可选的，在大多数未显式注解类型的情况下，编译器能自动导出值的类型。

```js
// 变量被自动推导为字符串类型 string
let variable = "hello";
// 等价于
let variable: string = "hello";

// 返回值被自动推导为数字类 number
function show(param: number) {
  return param;
}
// 等价于
function show(param: number): number {
  return param;
}
```

#### 类型查询

类型查询是一条语句，相当于一个独立类型。代码中任何需要显式注解得地方，都可以使用类型查询代替：

`:typeof 值`

在 js 中， typeof 是一个用来判断类型得关键字，在累心给查询语法中有相似的作用。

```js
// 声明 a 为 number
let a: number;

// 通过类型查询声明 b 的类型
let b: typeof a;
// 等价于
let b: number;

// 函数fn为函数
function fn() {}

// 通过类型查询声明 d 的类型为 fn 的类型d:()=
let d: typeof fn;
// 等价于
let d: () => void;
```

#### 总结

类型注解、类型推导、类型查询 构成了 TS 的类型判定系统，TS 编译器判定值得类型时，主要是用过以上的三种方式。

### 1.2 简单类型

#### 数字类型

数字类型关键字`number`，所有数字都是浮点数

```js
let intLiteral: number = 5;
let floatLiteral: number = 3.1415;
```

#### 布尔类型

```js
let isDone: boolean = false;
isDone = true;
```

#### 符号类型

```js
let sym: symbol = Symbol();
let sym1: symbol = Symbol("test");
```

#### void 类型

void 类型表示没有类型或者空类型。

当一个函数没有返回值时，你可以显示指定返回值为：`void`，如果不显示指定，会被自动推导为 `void`类型

```js
// 显式指定返回类型为 void
function sayHi(): void {
  // body..
}
// 等价
function sayHi() {
  // body..
}
```

显式声明一个值为 void 类型时合法的，但是没有意义，因为你只能为他赋值 `undefined`或 `null`

```js
let x: void = undefined;

// 仅在 strictNullChecks 编译选项关闭时合法
let y: void = null;
```

> 当把 `null` 赋值给 Void 类型 的时候，仅在 strictNullChecks 编译选项关闭时才合法

#### null 类型和 undefined 类型

undefined 和 null 都是可以作为其他类型的子类型出现的。（tsconfig.json 中严格模式关闭的情况下）

#### never 类型

#### any 任意类型

任意类型就是**可以被当作任何类型使用的的值**。

```javascript
// 声明为任意类型
let notSure: any = 4;

// 赋值为字符串类型
notSure = "hello world";

// 赋值为布尔类型
notSure = false;
```

一个值，如果满足以下任何一个条件，会被判定为任意类型：

1、显式指定类型 `any`

```javascript
// 显式指定变量类型，x为any
let x: any;

// 显式指定变量类型，y为any
let y: any = 10;
```

2、未显式指定类型，且没有初始化或默认值

```javascript
// 未指定类型，且未初始化。x为any
let x;

// 未指定类型，但初始化了。y被自动推导为number
let y = 10;

// 未指定类型，且没有默认值。参数x为any
function f(x) {
  console.log(x);
}
```

尽量不要使用 any 类型，any 类型表现上跟 JavaScript 的类型一样弱。TypeScript 最大的优势在于类型化带来的强约束作用，他可以让你更早的发现错误，并带来更高的可维护性

#### object 类型

`object`表示非原始类型，也就是除了`number`,`string`,`boolean`,`symbol`,`null`或`undefined`之外的类型。

使用`object`类型，就可以更好的表示`Object.create` 这样的 api

```js
declare function create(o: object | null): void;

create({ prop: 0 }); // ok
create(null); // ok

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

### 1.3 数组类型

#### 语法： `T[]`

`T`可以是任何类型，代表的是数组的元素类型

```js
let list: number[] = [1, 2, 3];

let list2: Array<number> = [11, 22, 33];

let list3: any[] = [1, 23, "asd", true];

// 二维数组
let vec: number[][] = [
  [1, 2, 3],
  [3, 4, 5],
];
```

### 元组类型

元组类型和数组类型相似，只不过元组是一种 **固定长度的数组**，**每个元素有自己的类型**。

#### 语法：`[T0, T1,...]`

`T0, T1`代表任意类型，省略号表示可以有任意多个元素

```js
// 声明一个元组，包含两个元素，第一个元素为 string 类型，第二个元素为 number 类型
let x: [string, number];
// 正确
x = ["hello", 10];

// 错误，元素类型不匹配
// error TS2322: Type 'number' is not assignable to type 'string'
// error TS2322: Type 'string' is not assignable to type 'number'
x = [10, "hello"];

// 错误；长度不匹配
// error TS2741: Property '1' is missing in type '[string]' but required in type '[string, number]'
x = ["hello"];
```

### 1.4 函数类型

在 js 中，函数可以作为一个整体辅助给一个变量。

```js
let fn = function () {};
```

既然函数可以作为值赋给变量，那么他就该有自己的类型。

```js
// ()=> void 是变量fn的类型，代表是一个函数类型。是fn的类型注解。
let fn: () => void;
fn = function () {};
```

#### 语法:

```js
// 这里的箭头 => 用于类型声明
(p1: T1, p2: T2,...) => T
```

#### 函数定义

在 ts 中，函数定义相对于 js 的区别就是可以显式的为参数和返回值添加类型注解。

```js
// js 函数定义

// 函数声明
function sum(a, b) {
  return a + b;
}

// 函数表达式
let fn = function () {};

// TS 函数定义
function sum(a: number, b: number): number {
  return a + b;
}
```

直接定义的函数有自己的隐式函数类型，比如上面的函数定义,函数会自动推导出 sum 函数具有的类型
：

```js
(a: number, b: number) => number;
```

通过类型查询，可以获取一个直接定义的函数的类型：

```ts
// 直接定义的函数
function sum(a: number, b: number): number {
  return a + b
}
// 通过 typeof 关键字火球函数 sum 的类型
// (a: number, b: number) => number
let fn: typeof sum

// 将类型兼容的函数赋值给 fn
fn = function (x: number, y: number): number {
  retunr x + y
}
```

#### 类型兼容

判断一个函数类型是否和一个函数兼容，只需要判断参数类型和返回值类型是否同时兼容

```js
// 声明 fn 为函数类型
let fn: (x: number, y: string) => boolean;

// 正确 参数名字不做兼容检查
fn = function (a: number, b: string): boolean {
  // ...
  return true;
};

// 正确 允许函值得参数比声明参数少
fn = function (a: number): boolean {
  // ...
  return true;
};

// 错误，函数返回值类型不匹配
// error TS2322: Type '(a: number, b: string) => string' is not assignable to type '(x: number, y: string) => boolean'
fn = function (a: number, b: string): string {
  // ...
  return b;
};

// 错误，参数过多
// error TS2322: Type '(a: number, b: string, c: number) => boolean' is not assignable to type '(x: number, y: string) => boolean
fn = function (a: number, b: string, c: number): boolean {
  // ...
  return true;
};

// 错误，参数类型不匹配，第二个参数应该为 string 类型
// error TS2322: Type '(a: number, b: boolean) => boolean' is not assignable to type '(x: number, y: string) => boolean'
fn = function (a: number, b: boolean): boolean {
  // ...
  return true;
};

// 错误，返回值类型不匹配，应该为 boolean
// error TS2322: Type '(a: number, b: string) => void' is not assignable to type '(x: number, y: string) => boolean'
fn = function (a: number, b: string): void {
  // ...
};
```

#### 可选参数

可选参数在挑用时可以不必传递，而必选参数在调用时必须传递。
在参数得类型注解前添加`?`即可让参数成为可选参数

```js
// 参数 a 必须，参数 b 可选，b 必须位于 a 之后
function test(a: number, b?: number): void {
  // ...
}

// 正确，忽略可选参数
test(1);
// 正确，传递可选参数
test(1, 2);

// 错误，必选参数 a 未传递
// error TS2554: Expected 1-2 arguments, but got 0
test();
```

必须注意的是**可选参数必须位于必选参数之后**，下面的定义就是不合法的：

```js
// 错误，可选参数之后不能有必选参数
// error TS1016: A required parameter cannot follow an optional parameter
function test(a?: number, b: number): void {
  // ...
}
```

#### 接口实现函数类型

接口能够描述 JavaScript 中对象得各种各样的外形。除了描述带有属性的普通对象外，接口也可以描述函数类型。

为了使用接口表示函数类型，我们需要给接口定义一个调用签名。他就像是只有参数列表和返回值类型的函数定义。参数列表里的每一个参数都需要名字和类型。

```javascript
// 接口可以描述函数类型（参数的类型和返回值的类型）
interface SearchFunc {
  (source: string, subString: string): boolean;
}
const mySearch: SearchFunc = function (source: string, sub: string) {
  return source.search(sub) > -1;
};
console.log(mySearch("abcd", "bc"));
```

### 1.5 枚举类型

```js
enum T { ... }
```

定义新的枚举类型，`T` 是任意定义得名字，省略号`...`表示可以定义一个或者多个显式初始化得枚举值。如：

```js
enum Direction {
    UP,
    Down,
    Left,
    Right
}
```

定义了新的枚举类型关键字`Direction`，现在可以用这个关键字声明新的枚举类型

```tsx
// 声明并初始化
let d: Direction = Direction.Down;
// 改变枚举类型的值
d = Direction.UP;
```

#### ....

### 1.6 复合类型

#### 交叉类型

```tsx
T1 & T2 & ...
```

交叉类型是将多个类型合并为一个总的类型，他包含了 **多个类型的所有特性**，类似于 **且**操作

```tsx
interface Bird {
  fly(): void;
}
interface Dog {
  run(): void;
}

// 同时具有Bird的fly和Dog的run特征
class Animal {
  fly() {}
  run() {}
}

// 正确

let animal: Bird & Dog = new Animal();
```

#### 联合类型

```tsx
T1 | T2 | ...
```

联合类型是取多个类型中的其中一个，只要满足其中一个类型，就认为类型兼容。类似于**或**操作。

```tsx
interface Bird {
  fly(): void;
}
interface Dog {
  run(): void;
}
// 与 Bird 兼容
class Animal1 {
  fly() {}
}
// 与 Dog 兼容
class Animal2 {
  run() {}
}
let animal1: Bird | Dog = new Animal1();
let animal2: Bird | Dog = new Animal2();
```

#### 高级联合

构成联合的组合可以是以下三种方式的 **任意组合**

- 值与类型
- 值与值
- 类型与类型

```tsx
// 值与类型混搭
let u: 99 | string | boolean
u = 'a'
u = 99
u = true
// 值与值混搭
let u = 'a' | 'b | 99
u = 'a'
u = 'b'
u = 99
// 类型与类型混搭
let u: number | string | boolean
u = 99
u = 'hello world'
u = false
```

#### keyof 关键字

```tsx
// T代表类型
keyof T
```

`keyof`关键字作用与类型，通过 **获取一个类型的所有属性名**，**生成一个新的字符串值的联合类型**

```tsx
interface Person {
  name: string;
  age: number;
}
// 通过 keyof 关键字 声明联合
let keyWord: keyof Person;
// 等价于
let keyWord: "name" | "age";

keyWord = "name";
keyWord = "age";
```

`keyof ` 关键字生成的是 **字符串值**的联合，每个字符串都是被获取类型`T`的键的索引名

### 1.7 接口类型

#### 对象类型

对象类型是 TS 类型系统中最复杂也是最重要的类型，对象类型主要用于描述复杂的数据类型：

```tsx
// 声明一个值为对象的字面量
let man = { name: "joye", age: 30 };
// 等价于
let man: { name: string; age: number } = { name: "joye", age: 30 };
```

属性之间可以用**分号**间隔，也可以用**逗号**间隔，甚至可以只用**换行符**间隔。

为了保持代码的可读性和规范，建议**声明的描述中采用分号进行间隔**，以此来区分**注解**和**值**。

#### 接口类型

对象类型是匿名的接口类型，对象类型没有名字，接口类型有名字。

接口类型相当于为对象类型声明了一个别名。

```tsx
// 定义接口类型 Person
interface Person {
  name: string;
  age: number;
}
// 声明变量 man 为 Person 接口类型
let man: Preson = { name: "joye", age: 30 };
// 等价于
let man: { name: string; age: number } = { name: "joye", age: 30 };
```

统一术语：**接口**代表**接口类型**，**匿名接口**代表**对象类型**

#### 可选类型

接口的属性是可选的，可选属性类似于函数的可选参数：属性名后面添加 ？ 即可

```tsx
interface Person {
  name: string;
  age: number;
}

// 错误，缺少必选属性 age
let man: Person = {
  name: "joye",
};
```

将 age 改为 可选属性：

```tsx
interface Person {
  name: string;
  // 问号， 表示声明了 可选属性
  age?: number;
}

// 正确
let man: Person = {
  name: "joye",
};
```

#### 只读属性

可以通过在属性名前添加`readonly`关键字，指定只读属性，只读属性只能在创建的时候对其赋值，一旦创建完成，就再也不能更改。

```tsx
interface Person {
  // 声明 name 为只读
  readonly name: string;
  age: number;
}

// 创建时 对只读属性赋值
let man: Person = {
  name: "joye",
  age: 30,
};

// 错误， 对只读属性的值不能更改
man.name = "rose";

// 正确， 非只读属性的值可以更改
man.age = 23;
```

#### 接口的应用

接口最重要的作用时描述一个**复杂值**的外形，通常可以描述：

- 对象字面量
- 函数
- 可索引值
- 类

##### 描述对象字面量

前面的 Person 接口就是描述对象字面量的例子。

对象字面量的类型匹配**非常让人迷惑**，请看下面的例子：

```tsx
interface Person {
  name: string;
  age: number;
}

// 定义一个对象字面量male
let male = {
  name: "joye",
  age: 30,
  gender: "male",
};

// 正确，male包含Person接口的所有属性
let man: Person = male;
```

在上面的例子中，对象字面量 `male` 被编译器推导为匿名接口类型，相当于：

```tsx
// 声明male为匿名接口
let male: {
  name: string;
  age: number;
  gender: string;
};
// 对male赋值
male = {
  name: "joye",
  age: 30,
  gender: "male",
};
```

匿名接口类型包含了 `Person` 接口的所有属性 `name`、`age`，编译器认为类型匹配，通过类型检查。**然而**:

```tsx
interface Person {
  name: string;
  age: number;
}

// 直接将对象字面量赋值给接口类型
// 错误，对象字面量直接赋值检查所有属性的兼容性
// error TS2322: Type '{ name: string; age: number; gender: string; }' is not assignable to type 'Person'.
// Object literal may only specify known properties, and 'gender' does not exist in type 'Person'.
let man: Person = {
  name: "joye",
  age: 30,
  gender: "male",
};
```

> 请牢记：对象字面量在**直接赋值**的时候，编译器会检查字面量类型是否**完全匹配**，多一个或少一个属性都会报错。

##### 描述函数

声明一个函数类型的多种方式：

```tsx
// 描述函数
interface MyFunc {
  (name: string, age: number): string;
}

// 声明接口类型
let fn: MyFunc;
// 等价于
// 匿名接口
let fn: { (name: string, age: number): string };
// 等价于
let fn: (name: string, age: numer) => string;

// 赋值
fn = function (name: string, age: number): string {
  return `$(name), $(age)`;
};
```

用接口描述一个带静态属性的函数

```tsx
// 定义 myFunc 函数
function myFunc() {}
// myFunc 具有静态属性 ‘test’
myFunc.test = "hello world";

// 声明接口类型描述函数 myFunc
interface MyFunc {
  // 描述函数定义
  (): voiod;
  // 描述静态属性 test
  test: string;
}

// 正确，类型匹配
let newFunc: MyFunc = myFunc;
```

##### 描述可索引值

可索引值一般表示数组类型和对象类型，可以通过 **键访问**某一项的值或者属性值。

###### 描述数组：

```tsx
// 描述一个数组
interface StringArray {
  [index: number]: string;
}
// 声明接口类型
let myArray: StringArray;
// 等价于
// 匿名接口
let myArray: { [index: number]: string };
// 等价于
let myArray: string[];

// 赋值
myArray = ["Bob", "Fred"];
```

###### 描述对象：

```tsx
// 描述一个对象
interface MyObject {
  [index: string]: string;
}

// 声明接口类型
let myObject: MyObject;

// 赋值
myObject = {
  a: "1",
  b: "2",
  c: "3",
};
```

对比前面描述对象字面量的语法，你会发现，这种方式描述对象可以**支持无限多的对象属性**，上述例子中：

```
// 省略号代表其他任意属性
myObject = {
  a: '1', b: '2', c: '3', d: '4', ...
}
```

##### 描述类数组对象

如果一个对象既支持数字索引，也支持字符串索引，这种对象在 JavaScript 中被称作**类数组对象**:

```
// 类数组对象
let obj = {
  1: 1,
  2: 2,
  name: 'joye',
  age: 30
}

obj[1] === 1;
obj[2] === 2;
obj['name'] === 'joye';
obj['age'] === 30;
```

实际上，当采用数字索引方式访问一个值时，JavaScript 会将数字索引转换为字符串索引:

```
obj[1] === 1;
obj[2] === 2;

// 完全等价于
obj["1"] === 1;
obj["2"] === 2;
```

在 TypeScript 中，接口类型可以同时描述数字索引类型和字符串索引类型：

```
// 正确
interface IndexObj {
    [x: number]: string;
    [x: string]: string;
}
```

但要注意，**由于 JavaScript 会将数字索引转换为字符串索引**，数字索引和字符串索引的**值的类型**必须相等，或者数字索引的返回值必须是字符串索引返回值类型的子类型：

```
// 错误，数字索引的值和字符串索引的值不匹配
// error TS2413: Numeric index type 'number' is not assignable to string index type 'string'
interface IndexObj {
    [x: number]: number;
    [x: string]: string;
}
```

##### 描述类

构造器类型代表的就是类本身。用接口来描述一个类：

```javascript
// 定义一个类
class NewClass {}

// 用接口来描述这个类类型
interface MyClass {
  new(): NewClass;
}

// 声明一个变量为描述这个类的接口类型并初始化
let myClass: MyClass = NewClass;
// 等价于
let myClass: typeof NewClass = NewClass;
```

##### 用类来实现接口

我们介绍到用接口来描述函数、可索引值、类类型，你会发现还不如直接用类型来声明更直接：

```js
// 声明函数
let myFunc: () => {};

// 声明数组
let myArr: string[];

// 声明类
class MyClass {}
let myClass: typeof MyClass;
```

在实际使用中的确是这样，我们很少直接用接口来声明一个函数或数组。接口更重要的场景在于可以被类实现，从而实现各种复杂的设计模式，在 TypeScript 中，接口可以被类实现

> 在面向对象的编程方法学中，接口对于代码可维护性和业务逻辑解耦起着至关重要的作用

```tsx
// ClockInterface 描述了一个属性和一个方法
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date): void;
}

// 实现接口
class Clock implements ClockInterface {
  constructor(h: number, m: number) {}

  currentTime: Date;
  setTime(d: Date) {
    this.currentTime = d;
  }
}
```

实现类必须包含接口所声明的**全部必选属性**，在上面的例子中：`Clock`类必须同时包含属性 `currentTime` 和方法 `setTime`：

```tsx
interface ClockInterface {
  currentTime: Date;
  setTime(d: Date): void;
}

// 错误，缺少属性 currentTime
// error TS2420: Class 'Clock' incorrectly implements interface 'ClockInterface'.
// Property 'currentTime' is missing in type 'Clock'
class Clock implements ClockInterface {
  setTime(d: Date) {}
  constructor(h: number, m: number) {}
}
```

#### 接口继承

```tsx
interface Shape {
  color: string;
}
interface Square extends Shape {
  sideLength: number;
}

// 正确，color 属性来自父接口
let square: Square = {
  color: "blue",
  sideLength: 4,
};
```

### 1.8 类类型

类本身就是一种类型，类的名字可以直接作为类型名：

```tsx
// 定义类
class TypeA {
  // ...
}

// 声明TypeA类型
let a: TypeA;
// 赋值TypeA类型
a = new TypeA();
```

#### 语法扩展

## 二、泛型

## 三、类型转换

### 类型别名

别名不会创建一个新的类型，它只是原类型的一个引用，和原类型完全等价，语法如下：

`type 别名 = 类型`

类型别名可以简化程序，可以提高可读性和课维护性，以下都是合法的类型别名声明：

```js
// 数字类型别名
type myNumber = number
// 布尔类型别名
type myBoolean = boolean
// 联合类型别名
type transiton = 'EASE' | 'EASEIN' | 'EASEOUT'
// 联合类型别名
type StringOrNumber = string | number
// 联合类型别名
type Text = string | {text: string}
// 泛型的实际类型别名
type NameLookup  = Directionay<string, Person>
// 通过类型查询定义别名
type ObjectStatics = typeof Object
// 泛型函数别名
type Callback<T> = (data: T) => void
// 元组泛型别名
type Pair<T> = [T, T]
// 泛型的实际类型别名
type Coordinates = Pair<number>
// 联合类型别名
type Tree<T> = T | {left: Tree<T>, right: Tree<T>

```

声明了别名以后，别名就相当于是一个`类型的标识符`，可以用于类型注解语法中。

```js
// 声明 transition 为联合类型的别名
type transition = "EASE" | "EASEIN" | "EASEOUT";
// transition 此时是一个类型的标识符
const boxTransition: transtion = "EASE";
```

### 类型断言

类型断言就是明确告诉编辑器一个值的类型，**相当于类型转换**，断言有两种语法格式：

```js
// 1. 尖括号语法
<类型表达式>值
// 2. as语法
值 as 类型表达式
```

> 两种形式是等价的。 至于使用哪个大多数情况下是凭个人喜好；然而，当你在 TypeScript 里使用 JSX 时，只有 `as`语法断言是被允许的。

```js
let someValue: any = 'this is a string'

// 1. 尖括号语法
let strLength: number = (<string>someValue).length

// 2. as语法
let strLength: number = (someValue as string).length
```

## 四、模块

## 五、命名空间

## 六、理解声明
