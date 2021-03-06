https://www.cnblogs.com/xiaohuochai/p/7243166.html

## 对象解构

### 普通解构

```js
let node = {
    type: 'boss',
    name: 'jerry'
}

// 普通解构
let {type, name} = node
// 解构时，指定的局部变量不存在，那么值为 undefined
let {type, name, value} = node
// 解构 赋默认值
let {type, name, value = true} = node
// 解构 赋 别名
let {type: localType, name: localName, value} = node
// 解构 赋 别名的同时，也可以赋默认值值
let {type: localType, name: localName = 'lucce', value} = node
```

### 嵌套对象的解构

解构嵌套对象仍然与对象字面量的语法相似，可以将对象拆解以获取想要的信息

```js
 let node = {
    type: "Identifier",
    name: "foo",
    loc: {
        start: {
            line: 1,
            column: 2
        },
    end: {
        line: 1,
        column: 4
    }
}
};

// 将 start 解构出来
let {loc: {start}} = node
// start.line =1  start.column = 2

// 同时也可以使用其他的别名 为解构出来的 对象属性命名
let {loc: {start: localStart}} = node
// localStart.line = 1 localStart.column = 2 
```

## 数组解构

#### 普通解构

```js
let colors = [ "red", "green", "blue" ];
let [ firstColor, secondColor ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"

let colors = [ "red", "green", "blue" ];
let [ , , thirdColor ] = colors;
console.log(thirdColor); // "blue"
```

#### 变量交换

```js
// 在 ES6 中互换值,不需要引入中间变量
let a = 1,
    b = 2;
[ a, b ] = [ b, a ];
console.log(a); // 2
console.log(b); // 1


```

#### 默认值

```js
let colors = [ "red" ];
let [ firstColor, secondColor = "green" ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

#### 嵌套数组解构

```js
let colors = [ "red", [ "green", "lightgreen" ], "blue" ];
// 随后
let [ firstColor, [ secondColor ] ] = colors;
console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

#### 不定元素

```js
let colors = [ "red", "green", "blue" ];
let [ firstColor, ...restColors ] = colors;
console.log(firstColor); // "red"
console.log(restColors.length); // 2
console.log(restColors[0]); // "green"
console.log(restColors[1]); // "blue"
```

> 注意:在被解构的数组中，不定元素必须为最后一个条目，在后面继续添加逗号会导致程序抛出语法错误

#### 数组赋值

```js
// 在 ES5 中克隆数组
var colors = [ "red", "green", "blue" ];
var clonedColors = colors.concat();
console.log(clonedColors); //"[red,green,blue]"

// 在 ES6 中克隆数组
let colors = [ "red", "green", "blue" ];
let [ ...clonedColors ] = colors;
console.log(clonedColors); //"[red,green,blue]"
```

### 混合结构

```js
let node = {
    type: "Identifier",
    name: "foo",
    loc: {
        start: {
            line: 1,
            column: 1
        },
        end: {
            line: 1,
            column: 4
        }
    },
    range: [0, 3]
};
let {
    loc: { start },
    range: [ startIndex ]
} = node;
console.log(start.line); // 1
console.log(start.column); // 1
console.log(startIndex); // 0
```

#### 解构参数

　解构可以用在函数参数的传递过程中，这种使用方式更特别。当定义一个接受大量可选参数的JS函数时，通常会创建一个可选对象，将额外的参数定义为这个对象的属性

```js
// options 上的属性表示附加参数
function setCookie(name, value, options) {
    options = options || {};
    let secure = options.secure,
        path = options.path,
        domain = options.domain,
        expires = options.expires;
        // 设置 cookie 的代码
}
// 第三个参数映射到 options
setCookie("type", "js", {
    secure: true,
    expires: 60000
});
```

### 解构的时候 重命名变量
```js

const metadata = {
  title: 'Scratchpad',
  translations: [
    {
      locale: 'de',
      localization_tags: [],
      last_edit: '2014-04-14T08:43:37',
      url: '/de/docs/Tools/Scratchpad',
      title: 'JavaScript-Umgebung'
    }
  ],
  url: '/en-US/docs/Tools/Scratchpad'
};
 
let {
  title: englishTitle, // rename
  translations: [
    {
       title: localeTitle, // rename
    },
  ],
} = metadata;
 
console.log(englishTitle); // "Scratchpad"

```