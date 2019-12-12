## __proto__的默认指向 	


简书[https://www.jianshu.com/p/686b61c4a43d]
虽然JavaScript里一切皆对象，但为了理解原型链系统，我们需要将JavaScript的对象分为对象和函数两大类。在此基础上，JavaScript的原型链逻辑遵从以下通用规则：

通用规则:
对象有__proto__属性，函数有prototype属性；
对象由函数生成;
生成对象时，对象的__proto__属性指向函数的prototype属性。
在没有手动修改__proto__属性的指向时，以上三条便是JavaScript默认原型链指向逻辑。

下面我们来从最一般的情况开始，逐步深入的详细解释一下：
```js

### 1. 一般情况

创建空对象时，实际上我们是用Object函数来生成对象的：
var o = {}
o.__proto__ === Object.prototype
true

我们也可以显式的使用Object函数来创建对象：
>var o = Object()
o.__proto__ === Object.prototype
true

当我们使用函数来创建自定义的对象时，上面的规则同样适用：
>function MyObj(){}
>typeof MyObj
"function"
>var mo = new MyObj()
>mo.__proto__ === MyObj.prototype
true
```
2. 函数对象
既然JavaScript里“一切皆对象”，那函数自然也是对象的一种。对于函数作为对象来说，上面的规则同样适用：
```js

函数对象都是由Function函数生成的：
>function fn(){}
>fn.__proto__ === Function.prototype
true
我们可以看到，把函数当做对象时，生成它的函数就是 Function函数。那Function函数本身呢？同样适用！

Function函数本身作为对象时，生成它的函数是他自身！
>Function.__proto__ === Function.prototype
true
同样我们知道，Object函数也是一个函数对象，那么它是否符合上面的规则呢？当然！

Object函数既然是函数，那生成它的函数自然是Function函数咯：
>Object.__proto__ === Function.prototype
true
```
3. prototype是谁？
好了，现在我们知道，对象的__proto__属性是从生成它的函数的prototype那里得来的，那我们不禁要问，函数的prototype又是谁？
```js
一般函数默认的prototype是系统自动生成的一个对象：
>function fn(){}
>typeof fn.prototype
"object"
>fn.prototype
{constructor: ƒ}
    constructor: ƒ fn()
    __proto__: Object

>fn.prototype.constructor === fn
true
>fn.prototype.__proto__ === Object.prototype
true
```
一般函数默认的prototype是一个类型为"object"的对象，它有两个属性：constructor和 __proto__。其中constructor属性指向这个函数自身，__proto__属性指向Object.prototype，这说明一般函数的prototype属性是由Object函数生成的。


4. 特殊情况
前面我们特别强调了是一般函数，那不一般的函数是谁呢？当然是Object函数和Function函数！
先来看Object.prototype:

>typeof Object.prototype
"object"
>Object.prototype
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
    constructor: ƒ Object()
    hasOwnProperty: ƒ hasOwnProperty()
    isPrototypeOf: ƒ isPrototypeOf()
    propertyIsEnumerable: ƒ propertyIsEnumerable()
    toLocaleString: ƒ toLocaleString()
    toString: ƒ toString()
    valueOf: ƒ valueOf()
    __defineGetter__: ƒ __defineGetter__()
    __defineSetter__: ƒ __defineSetter__()
    __lookupGetter__: ƒ __lookupGetter__()
    __lookupSetter__: ƒ __lookupSetter__()
    get __proto__: ƒ __proto__()
    set __proto__: ƒ __proto__()
可以看到Object函数的prototype属性也是一个类型为"object"的对象，但和一般函数的默认prototype属性不一样的是，它多了一大堆方法，这些方法都是JavaScript对象的系统默认方法。
再仔细看，好像少了什么，对了，Object函数的prototype属性里没有__proto__属性，我们试着把它的__proto__属性打出来看看：

>Object.prototype.__proto__
null
这就是Object函数特殊情况了：Object.prototype.__proto__ === null，我们知道，这就是JavaScript原型链的终点了。
为什么要这样设定呢？
typeof Object.prototype === "object"，说明它是一个Object对象，如果它由Object函数生成，于是按照我们上面的通用规则，就该是Object.prototype.__proto__ === Object.prototype。
啊哈，问题出现了，Object.prototype.__proto__属性指向了它自身，这样以__proto__属性构成的原型链就再也没有终点了！所以为了让原型链有终点，在原型链的最顶端，JavaScript规定了Object.prototype.__proto__ === null。

好，现在再来看Function函数吧：

>typeof Function.prototype
"function"
一上来就不走寻常路，Function函数的prototype属性是一个"function"类型的对象，而不像其他函数是类型为"object"的对象。那是个什么样的函数呢？

>Function.prototype
ƒ () { [native code] }
函数内部是[native code]，也就是系统编译好的二进制代码函数，这就暂时没法深究了。现在让我们来看看我们最关心的__proto__属性：

>Function.prototype.__proto__
{constructor: ƒ, __defineGetter__: ƒ, __defineSetter__: ƒ, hasOwnProperty: ƒ, __lookupGetter__: ƒ, …}
    constructor: ƒ Object()
    hasOwnProperty: ƒ hasOwnProperty()
    isPrototypeOf: ƒ isPrototypeOf()
    propertyIsEnumerable: ƒ propertyIsEnumerable()
    toLocaleString: ƒ toLocaleString()
    toString: ƒ toString()
    valueOf: ƒ valueOf()
    __defineGetter__: ƒ __defineGetter__()
    __defineSetter__: ƒ __defineSetter__()
    __lookupGetter__: ƒ __lookupGetter__()
    __lookupSetter__: ƒ __lookupSetter__()
    get __proto__: ƒ __proto__()
    set __proto__: ƒ __proto__()
怎么有种似曾相识的感觉呢？看起来很像是Object.prototype，让我们来试试：

>Function.prototype.__proto__ === Object.prototype
true
果然就是它！
按照我们最开始提出的通用规则，一个"function"类型的对象，应该是由Function函数生成的，那它的prototype属性应该指向Function.prototype，也就是Function.prototype.__proto__ === Function.prototype。和Object函数同样的问题出现了：循环引用。所以JavaScript规定Function.prototype.__proto__ === Object.prototype，这样既避免了出现循环引用，又让__proto__构成的原型链指向了唯一的终点：Object.prototype.__proto__ === null。

5. 总结
至此，我们从最一般的对象一直追溯到了Object函数和Function函数，并找在原型链的顶端发现了两个例外情况，也知道了这两个例外个规定是为了让__proto__构成的原型链存在一个唯一的终点。

现在我们再来看这张JavaScript原型链的图，是不是一目了然了呢？

![__proto__](https://upload-images.jianshu.io/upload_images/13902845-babea8f0cde0d791.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)