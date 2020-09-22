## constructor 构造函数

constructor() 方法是类的构造函数（默认方法），用于传递参数，返回实例对象，通过 new 命令生成对象的实例时，自动调用该方法。如果没有显式定义，类内部会自动给我们创建一个 constructor()

1. class 关键子创建类，类名习惯性大写首字母
2. 类里面有一个 constructor 函数，可以接收传递过来的参数，同时返回实例对象。
3. constructor 函数， 只要 new 生成实例，就会调用这个函数，如果不写这个函数，系统会自动生成这个函数
4. 生成实例 new 不能省略
5. 注意语法规范，创建类 后面是 花括号，new 生成实例时， 后面是 小括号， 构造函数不需要加 function

### 继承

1. extends 继承 

2. super() 

   super 关键字用于访问和调用父类对象上的函数。可以调用父类的构造函数，也可以调用父类的普通函数。

```js

class Father {
    constructor(name, pass) {
        this.name = name
        this.pass = pass1
    }
    showName() {
        console.log(this.name)
    }
}
class Son extends Father { // extends 关键字 继承
    constructor(name, pass, sex) {
        super(name, pass) // super 访问父类上的变量
        this.sex = sex
    }
    showSex() {
        console.log('i am a boy!')
    }
}
```

