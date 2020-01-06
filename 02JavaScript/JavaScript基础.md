## 一、js基础概念

### 浏览器执行js的过程

渲染引擎（内核）

js引擎（js解释器）

逐行解释，转换为机器语言，然后由计算机执行

### js的组成和书写位置、

组成三部分：

1. ECMAScript
    语言标准，编程语法和基础核心知识。
2. DOM
    文档对象模型。
    操作元素，大小、位置、颜色等
3. BOM
    浏览器对象模型
    操作窗口，控制页面效果
    弹出框、分辨率等

三种书写位置：
    1. （内嵌式）
    head里面

    head外面
    
    body里面
    
    2. 行内（点击按钮里的js代码）
    
    3. 外部js文件

## 二、js变量

### 变量的三种声明方式：

- var ：声明一个变量，可选初始化一个值。

- let ：声明一个块作用域的局部变量，可选初始化一个值。

- const ：声明一个块作用域的只读常量。

- 如果只是声明变量而没有赋值，则该变量的值是`undefined`。`undefined`是一个特殊的值，表示“无定义”。

- JavaScript是动态型语言，也就是说变量的类型没有限制，变量可以随时改变类型。
  
  ### 变量提升
  
  javascript引擎的工作方式是，先解析代码，获取所有被声明的变量，然后在一行一行的运行。这造成的后果就是所有变量的声明语句，都会被提升到代码的头部，这就叫做变量的提升（hoisting）。

## 三、数据类型

### 六种数据类型：

一：基本数据类型 String Number Boolen Null undefined  
二：引用数据类型 Object

***ES6又新增加了一种symbol类型的值***

- String 字符串 文本
- number 整数和小数
- boolean 
    表示真伪的两个特殊值 true false
- undefined     
    表示未定义或者不存在，即由于目前没有定义，所以此处没有任何的值
- null 表示空值。即此处的值为空
- object 对象 各种值组成的集合

>  对象是复杂的数据类型，又可以分成三个子类型。
> 
> - 狭义的对象（Object）
> - 数组（Array）
> - 函数（Function）

*狭义的对象和数组是两种不同的数据组合方式*

*函数其实是处理数据的方法，JavaScript把它当成一种数据类型，可以赋值给变量，这给JavaScript的“函数式编程”奠定了基础*

原始值 是存在栈内存里面的（stack）， first in，last out。
引用值值存在堆内存里面的（heap）。

### typeof运算符

JavaScript中有三种方式确定一个值到底是什么类型的。

- typeof 运算符
- instanceof 运算符
- Object.prototype.toString 方法

typeof运算符的返回值：

- 数值，字符串，布尔值分别返回`number` `string` `boolean` 
- 函数返回 `function`
- `undefined` 返回 `undefined` ,因此如果使用`typeof`检测一个没有声明的变量时,不会报错，但是如果直接使用没有声明的变量的话，是会报错的。
- 对象返回 `object`, 数组 `[]` 的类型也是 `object`,这意味着在JavaScript内部，数组本质上是一种特殊的对象。但是`instanceof`运算符是可以区分数组和对象的。
- `null` 返回 `object`，把null当做对象，是有历史原因的，JavaScript语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串、布尔值），没有考虑`null`,只把他当做`object`的一种特殊值，后来`null`独立出来，作为一种单独的数据类型，为了兼容以前的代码，`typeof null`返回`object`就无法改变了。

### null和undefined

- null和undefined都可以表示没有，将一个变量赋值为undefined或者null，在语法上是没有区别的。在if语句中，他们都会被自动转化为 `false` `==`运算符 报告二者相等。
  设计的区别是；`null`是一个表示“空”的对象，转化数值为`0`;`undefined`是一个表示“此处无定义”的原始值，转化数值时值为`NaN`。

- null 表示空值，即该处的值现在为空。调用函数时，某个参数未设置任何职没这事就可以传入`null`,表示该参数为空，

- undefined 表示“未定义”；
  1.变量声明了，但是没有赋值 undefined
  2.调用函数时，应该提供参数没有提供，该参数等于 undefined
  3.对象没有赋值的属性 undefined
  4.函数没有返回值，默认返回 undefined

### 布尔值

如果Javascript预期某个位置应该是布尔值，会将该位置上现有的值自动转化为布尔值。转化规则是除了下面六个值被转为`false`,其他的值都视为`true`。

- undefined
- null
- false
- 0 
- NaN
- 反引空字符串 或者''（空字符串）

> 注意： 空数组 [] 和 空对象 {} 对应的布尔值，都是 true

### 数值

JavaScript内部，所有数字都以64位浮点数形式存储，即使整数也是这样
` 1 === 1.0  // true `  1 和  1.0 是同一个数

### NaN

`NaN` 是javascript的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

- 需要注意的是：`NaN` 不是独立的数据类型，二十一个特殊数值，他的数据类型依然是`Numbber`,使用`typeof`运算符可以看得很清楚。

- NaN 不等于 任何值，包括他本身。

- NaN 在布尔运算时，被当作 `false`

- NaN 与任何数（包括自己）的运算，得到的都是 `NaN`
  
  ### isNaN()
  
  `isNaN()` 方法可以判断一个值是否是 `NaN`
  
  ```
  isNaN(NaN)  // true 
  isNaN(123)  // false 
  ```
  
  `isNaN()` 只对数值有效，传入其他值会想转数字，再进行判断
  
  ```
  isNaN('hello')` // true
  // 相当于
  isNaN(Number('hello')) // true
  ```
  
  ### 与数值相关的全局方法

- `parseInt()` 用于将字符串转为整数。
  
  ```
  
    parseInt('123')  // 123
    parseInt('  41') // 81 ,如果字符串头部有空格，空格会被自动去除
    parseInt(1.23)  // 1 如果参数不是字符串，则会先转为字符串再转换
    // 字符串转为整数的时候，是一个个的字符一次转换，如果遇到不能转为数字的字符，就不在进行下去，返回已经转好的部分
    parseInt('8a')  // 8
    parseInt('12**') // 12
    parseInt('15px29') // 15
    // 如果字符串的第一个自反不能转化为数字（后面跟着数字的正负号除外），返回 `NaN`
    parseInt('abc') // NaN
    parseInt('.3') // NaN
    parseInt('+') // NaN
    parseInt('+1') // 1
    // oX ox 开头 按照 16进制 解析
    parseInt('oX10')  // 16
    parseInt('015')  // 15
    // 科学计数法 视为字符串,就很奇怪，小数点后七位开始 出现这种情况 ,22位数出现
    parseInt(1000000000000000000000.5) // 1 
    parseInt('8e-7')  // 8 
    parseInt(0.0005)  // 5 
  ```

- Number() 和parseInt():
  Number("123asd") --->NaN
  parseInt("123asd") --->123

### 字符串

#### 字符串可以是对象

字符串是原始值，可以使用字符创建： var x = 'Lost is and let is go.' 
也可以用对象创建： var y = new String('Lost is and let is go.')
x != y , 因为一个是对象一个是字符串

#### 字符串的属性

- constructor 返回创造字符串的函数
- length 返回字符串的长度
- prototype 字符串的原型

#### 字符串的常用方法

## 数组精讲

###　数组的方法：

> 改变原数组
> 
> - push(arg) 
>     往原数组中添加arg
> 
> - prop
>     删除原数组中的最后一位
> 
> - unshift(arg)
>     在数组的最前面添加arg
> 
> - reverse()
>     反转数组
> 
> - splice(从第几位开始，截取的长度，在切口处添加新的数据)
>     截取数组
> 
> - sort()
>     数组排序，参数可以传入一个规则
>   不改变原数组
> 
> - concat()
>     连接两个数组，产生新的数组
> 
> - join(“-”)
>     参数为字符串，将原数组转化成字符串，按照传入的参数连接
> 
> - split()
>     将字指定符串转化成数组，按照传入的参数，拆分组合成数组
> 
> - toString()
>     把数组变成字符串
> 
> - slice()
>     截取数组:
>   
>         - slice(a,b) 从第a位开始截取，截取到第b位，[a, b）
>         - slice(a) 从a位开始，截取到最后一位
>         - slice(-a) 截取倒数共a位 
>         - slice() 截取全部    

### 类数组

- 可以利用属性名模拟数组的特性
- 可以动态的增长length属性
- 如果强行让类数组调用 push 方法，则会根据length属性值的位置进行属性的扩充。

## 对象

### 原型

## 函数

## 事件

### js获取样式

- 元素的可见宽高，包括内容和内边距
  
    clientWidth
  
    clientHeight

- 整个元素的宽高，包括内容区域和内边距外，边框
  
    offsetWidth 
  
    offsetHeight

- offsetLeft 当前元素相当于其定位父元素的水平偏移量
  
   offsetTop 当前元素相当于其定位父元素的垂直偏移量

- 可以获取元素整个可滚动区域的宽度高度
  
    scrollHeight
  
    scrollWidth

- scrollHeight - scrollTop == clientHeight  证明滚动条到底了

### 事件对象

#### 鼠标相关

- 鼠标坐标 
    e.clinetX e.clientY
    e = event || window.event

- div随着鼠标位置移动
    当出现 滚动条的时候：
    left = clientX + scrollLeft 
    top = clientY + scrollTop 
  
  ### 事件的冒泡（bubble）

event = event || window.event
取消冒泡 event.cancelBubble = true

### 事件的委派（事件的委托）

this 指的是 绑定事件的对象
event.target 返回触发事件的对象，大写

```js
ul.addEventListener("click",function(event){

    var target = event.target;
    //防止父元素ul也触发事件
    if(target.nodeName == "LI"){
        target.style.backgroundColor = "red";
    }
})
```

### 取消冒泡或默认行为

```js
//冒泡：
return false
或者
e.stopPropagation()
// 默认行为
e.preventDefault()
return false
```

### 自动触发事件

```js
obj.trigger()
obj.triggerHandler() // 会取消冒泡和默认事件
```

### 多个事件的绑定 addEventListener

***ie8及以下不支持，使用attachEvent代替***

- addEventListener 三个参数：
  
    1、事件的字符串，不要 on
  
    2、回调函数，当事件触发的时候调用
  
    3、是否在捕获阶段触发事件，需要一个布尔值，一般都传false

- attachEvent 
  两个参数： 
  
    1、事件的字符串 要on
  
    2、回调函数
  
    *注意：此方法绑定的事件，执行顺序是后绑定先执行*

- attachEvent 中的this 是window ，addEventListener 中的this 是绑定事件的对象

- 统一attachEvent和addEventListener中this的指向
  
  ```javascript
    /*
    * obj 是调用事件的对象，
    * eventStr 是 事件的字符串 ，
    * callback 是回调函数 
    */
    function bind(obj, eventStr, callback){
        if(obj.addEventListener){
            obj.addEventListener(eventStr, callback, false);
        }else{
            obj.attachEvent(eventStr, function(){
                callback.call(obj);
            })
        }
    }
  ```

### 事件的传播

- 关于事件的传播网景公司和微软公司有不同的理解。
- 微软公司认为事件应该是由内往外传播，也就是当事件触发时，应该先触发当前元素上的时间，然后再向当前元素的祖先原始上传播，也就是说时间应该在冒泡阶段执行。
- 网景公司认为事件应该是由外向内传播的，也就是当前事件触发时，应该先触发当前元素的最外层的祖先元素的事件，然后再向内传播给后代元素。
- W3C 综合了两个公司的方案，将事件传播分成了三个阶段
  - 1、捕获阶段：在捕获阶段时从最外层的祖先元素，向目标元素进行时间的捕获，但是默认此时不会触发事件。
  - 2、目标阶段：事件捕获到目标元素，捕获结束。开始在目标元素上触发事件。
  - 3、冒泡阶段：事件从目标元素向祖先元素传递，分别依次触发祖先元素上的事件。
- 如果希望在捕获阶段触发事件，可以将addEventListener()的第三个参数，设置为 true，一般情况下，不会希望在捕获阶段，执行事件，所以一般设置为false 
- IE8及以下的浏览器中没有捕获阶段
