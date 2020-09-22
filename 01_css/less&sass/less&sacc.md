## 预编译器介绍
### less：
node编写，编译快。

### scss：
ruby编写，编译慢，但是有node版本，使用c++编写，`node-scss`。

## 编译
都有自家的编译命令。
less: lessc
scss: node-sass
	默认编译会采用类似嵌套的形式展示，可以在编译命令加上 `-output-style expanded`, 取消默认嵌套形式

## 嵌套

> 反应层级和约束。

```css
.wrapper{
	width: 1000px;
	.nav{
		width: 100%;
	}
	&:hover{
		font-size: 14px;
	}
}
```
> less、scss的嵌套都是一样的

## 变量和计算

> 减少重复代码。便于维护。

less:
``` less
@fontSize: 12px;
@bgclolr: red;

.wrapper{
	background: ligthen(@bgcolor, 40%); // 设置透明度
	.nav{
		font-size: @fontSize;
	}
	.content{
		font-size: @fontSize + 2px; // 简单运算
	}
}
```
scss:
```scss
$fontSize: 12px;
$bgclolr: red;

.wrapper{
	background: ligthen($bgcolor, 40%); // 设置透明度
	.nav{
		font-size: $fontSize;
	}
	.content{
		font-size: $fontSize + 2px; // 简单运算
	}
}
```
## mixin

> 代码片段。

less:
```css
@fontSize: 12px;
@bgclolr: red;

.block(@fontSize){
	font-size: @fontSize;
	border: 1px solid #ccc;
	border-radius: 4px;
}
.wrapper{
	background: ligthen(@bgcolor, 40%); // 设置透明度
	.nav{
		.block(@fontSize); // 不会添加类名，只会引用其中的样式代码。类名加上括号就会这样应用，类似函数调用的引用
		font-size: @fontSize;
	}
	.content{
		// font-size: @fontSize + 2px; 
		.block(@fontSize);
		&:hover{
			background: red;
		}
	}
}
```
scss:
```css
$fontSize: 12px;
$bgclolr: red;

@maxin block($fontSize){
	font-size: $fontSize;
	border: 1px solid #ccc;
	border-radius: 4px;
}
.wrapper{
	background: ligthen(@bgcolor, 40%); // 设置透明度
	.nav{
		@include block(@fontSize); // 不会添加类名，只会引用其中的样式代码。类名加上括号就会这样应用，类似函数调用的引用
		font-size: $fontSize;
	}
	.content{
		@include block($fontSize + 2px);
		&:hover{
			background: red;
		}
	}
}
```
## extend

> 代码片段。

less:
```css
@fontSize: 12px;
@bgclolr: red;

// 需复用的公共样式
.block(@fontSize){
	font-size: @fontSize;
	border: 1px solid #ccc;
	border-radius: 4px;
}
.wrapper{
	background: ligthen(@bgcolor, 40%); // 设置透明度
	.nav:extend(.block()){
		font-size: @fontSize;
	}
	.content{
		&:extend(.block(@fontSize));
		&:hover{
			background: red;
		}
	}
}
```
scss:
```scss
$fontSize: 12px;
$bgclolr: red;

// 需要复用的公共样式
.block{
	font-size: $fontSize;
	border: 1px solid #ccc;
	border-radius: 4px;
}

.wrapper{
	background: ligthen(@bgcolor, 40%); // 设置透明度
	.nav{
		 @extend .block;
		font-size: $fontSize;
	}
	.content{
		@extend .block;
		&:hover{
			background: red;
		}
	}

}
```
## loop

> 适用于复杂有规律的样式。

例子：

生成网格样式：

```css
.col-12{
    width: 1000px;
}
.col-11{
    width: 916.6667px;
}
....
.col-3{}
.col-2{}
.col-1{}
```



less:

less 中没有循环，采用 `递归思想`实现。循环调用自己。

```less
.gen-col(@n) when (@n > 0){ // 定义出口，n > 0 , 当 n <= 0 结束
    .gen-col(@n - 1);
    .col-@{n}{
        width: 1000px/12*@n;
    }
}

.gen-col(12);
```

sass:

同样使用递归思想实现。

```scss
@mixin gen-col($n){
    @if $n > 0 {
        @include gen-col($n - 1);
        .col-#($n){
            width: 1000px/12*$n;
        }
    } 
}
@include gen-col(12);
```

sass:

使用循环实现。

```sass
@for $i from 1 through 12 {
    .col-#($i) {
        width: 1000px/12*$n;
    }
}
```

## import

> css文件模块化。

css 中是有`import` 语法的.

```css
@import "./section-1.css"
@import "./section-2.css" 
```

不会合并加载，造成网络负担。

### less:

main.less

```less
import "./variable"
import "./modelu1"
import "./modelu2"
```

variable.less

```less
@themeColor: cyan;
@fontSize: 14px;
```

modelu1.less

```less
.module1{
    .box{
        font-size: @fontSize + 2px;
        color: @themeColor;
    }
    .tips{
        font-size: @fontSize;
        color: ligthen(@themeColor, 40%)
    }
}
```

modelu2.less

```less
.module2{
    .box{
        font-size: @fontSize + 4px;
        color: @themeColor;
    }
    .tips{
        font-size: @fontSize + 2px;
        color: ligthen(@themeColor, 20%)
    }
}
```

### sass

使用方式和less一样。