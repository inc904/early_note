**一、定义类**

ES5没有class关键字，所以定义类要麻烦一点。

```
var Person = (function () {



    function Person(name) {



        this.name = name;



    }



    Person.prototype.SayHello = function () {



        window.alert("My name is " + this.name + ".");



    };



    return Person;



})();
```

上面的代码定义了一个名称为Person的类，它有构造函数、成员name、成员函数SayHello。

使用方法和通常的面向对象语言（如C#）很像：

```
var p = new Person("华盛顿");



p.SayHello();
```



**二、继承**

继承就更麻烦了，先要搞一个辅助变量：

```
var __extends = (this && this.__extends) || function (d, b) {



    for (var p in b) if (b.hasOwnProperty(p)) d[p] = b[p];



    function __() { this.constructor = d; }



    d.prototype = b === null ? Object.create(b) : (__.prototype = b.prototype, new __());



};
```

然后进行继承，下面的Fish继承了Animal。

```
var Animal = (function () {



    function Animal() {



    }



    Animal.prototype.Eat = function () {



        window.alert("Animal eat.");



    };



    return Animal;



})();



 



var Fish = (function (_super) {



    __extends(Fish, _super);



    function Fish() {



        _super.apply(this, arguments);



    }



    Fish.prototype.Eat = function () {



        window.alert("Fish eat.");



    };



    return Fish;



})(Animal); // 继承谁，就把谁传入
```

