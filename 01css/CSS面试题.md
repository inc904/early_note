## CSS 引入位置

外部样式表，引入一个外部 css 文件
内部样式表，将 css 代码放在 <head> 标签内部
内联样式，将 css 样式直接定义在 HTML 元素内部

## 行内元素和块级元素

### 块元素：

总是独占一行，宽高内外边距 都可以编辑

### 行内元素：

都在同一行。

### 行内块级元素：

拥有内在尺寸，可设置高宽，
但不会自动换行

```html
<input> 、<img> 、<button> 、<texterea> 、<label>
```



## CSS盒模型

盒模型：又叫框模型（Box Model ），包含了元素内容（content）、内边距（pading），边框border）、外边框（margin）四要素。

### 标准盒模型

![img](https://mmbiz.qpic.cn/mmbiz/vO7l6lQ0BwoyXkCumvC2M3IoMuw0Q37r3qCiaDuaqQ572y9somVO56iccFgUz04vpy4rXnZ4JJLCJZq0kJ7BKHTQ/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

盒子的内层是 content，依次是 padding、border、margin。

通常设置背景时，。是内容、内边距、边框这三个部分，如果border设置了颜色，就会显示 border 的颜色，当 border 的颜色是透明的时候，会显示 background-color 的颜色。 

元素内容的宽度是 width，

元素所占空间是 width+padding+border+margin

### IE盒模型

![img](https://mmbiz.qpic.cn/mmbiz/vO7l6lQ0BwoyXkCumvC2M3IoMuw0Q37rcIJzCSMRBAWjibzlLFKSjdmFfgpgIoXG83JgEPcXHYicUKZZcPzXSHgQ/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

元素所占内容宽度是包含 content+padding+ border

## CSS选择器

- 通用选择器： * {}
- id选择器：#header {}
- class选择器：.header {}
- 元素选择器：div {}
- 子元素选择器：ul>li {}
- 后代选择器：div p {}
- 伪类选择器：
  - hover {}
  - :first-child{}
  - :first-of-type
  - :nth-of-tyoe
- 伪元素选择器：
  - :after{}
  - :before {}
- 属性选择器：input[type="text"]
- 组合选择器 
  - 同级别群组选择器：E,F {}
  - 直接相邻：E+F {}
  - 普通相邻：E~F {}

## CSS属性的继承性

CSS能继承的特性主要是文本方面的继承（比如字体、颜色、字体大小），盒模型相关的属性基本没有继承特性。

## 常用的`@`规则

```css
/*定义字符集*/
@charset "utf-8"
/*导入css文件*/
@import "base.css"
/*自定义字体*/
@font-face {}
/*声明CSS3 animation动画关键帧*/
@keyframes fadeIn {}
/*媒体查询*/
@media{}
```



## CSS伪类和伪元素

### 伪类：

- :hover
- :active
- :first-child
- :visited
- 等

### 伪元素：

- :after
- :before
- :first-line
- :first-letter

### 伪类和伪元素的根本区别：

是否创造了新的元素。

### 实际应用

伪类一般用一个冒号表示：`:first-child`

伪元素一般两个冒号表示：`::after`

## CSS定位规则

### static 普通流定位

默认定位

### float 浮动定位

左浮动和右浮动两个值。

浮动元素会在没有浮动元素的上方展示，效果上看是遮挡住了没有浮动的元素。

有float 样式的元素是脱离文档流的。他的父元素的高度不能由他撑开。

### relative 相对定位

相对本元素的左上角进行定位。

top、left、botton、right 都可以有值。

经过定位后，位置可能会移动，但是本元素没有脱离文档流，还会占据原来的页面空间。

### absolute 绝对定位

position: absolute

相对于 `祖代`有relative 定位的元素定位，层级关系最近的元素的左上角进行定位。

如果祖代元素中没有 relative 定位的，就默认相对于 `body`进行定位。

绝对定位是 脱离文档流的。会压在非定位元素上方。

可以设置 z-index 值。

## **雪碧图实现原理：**

CSS雪碧的基本原理是把你的网站上用到的一些图片整合到一张单独的图片中，从而减少你的网站的HTTP请求数量。该图片使用CSS background和background-position属性渲染，这也就意味着你的标签变得更加复杂了，图片是在CSS中定义，而非<img>标签。

## 水平居中的方案

### 行内元素居中：

看他的 父级 是不是 块级 元素，如果是  直接给父元素 加 `text-align: center;`

如果不是，先将父元素设置成 块级元素，然后再加 `text-align`

### 块级元素水平居中（定宽度）

1. 需要谁居中，给谁设置`margin: 0 auto;`，使盒子自己居中。
2. 首先设置父元素为相对定位，再设置子元素为绝对定位，设置子元素的 `left:50%;`使得元素的左上角水平居中，然后设置子元素的`margin-left: -子元素的宽度的一半 px`，或者`transform:translateX(-50%)`

### 块级元素水平居中（不定宽度）

1. 默认子元素的宽度和父元素一样，这时需要设置子元素为display: inline-block; 或 display: inline;即将其转换成行内块级/行内元素，给父元素设置 text-align: center;
2. `transform: translateX(-50%);`

### Flex 布局水平居中（宽度定不定都可以）

```css
.ather{
    dispaly: flex;
    just-content: center;
}
```

## 垂直居中

### 单行的行内元素

行高等于盒子高度

### 多行的行内元素

```css
.father{
    dispaly: table-cell;
    vertical-align: middle;
}
```

### 块级元素垂直居中

#### 绝对定位

子绝父相，子： top: 50%

然后 margin-top: - 高度的一半 或者 `transform: translateY(-50%);`

#### flex布局

```css
.father{
    display: flex;
    align-item: center;
}
```



## 水平垂直居中

### 定位属性

子绝父相，子元素 设置 `left: 50%; top: 50%; transform: translateX(-50%) translateY(-50%);`

### flex 布局

```css
.father{
    dispaly: flex;
    justify-content: center;
    align-item: center;
}
```

## BFC布局规则

块级格式化上下文，他是一个独立的渲染区域，与外部毫不相干。

### 布局规则：

1. 内部的Box会在垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
3. 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
4. BFC的区域不会与float box重叠。
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
6. 计算BFC的高度时，浮动元素也参与计算

### **BFC的作用及原理：**

 1. 自适应两栏布局

 2. 清除内部浮动

 3. 防止垂直 margin 重叠

`BFC`内部的元素和外部的元素绝对不会互相影响，因此， 当`BFC`外部存在浮动时，它不应该影响`BFC`内部Box的布局，`BFC`会通过变窄，而不与浮动有重叠。同样的，当`BFC`内部有浮动时，为了不影响外部元素的布局，`BFC`计算高度时会包括浮动的高度。避免margin重叠也是这样的一个道理。

## CSS函数

属性函数：attr()； 

背景图片函数： url()

数学函数：calc()、min()、max()、mixmax()、repeat()；

## **PostCSS、Sass、Less的异同，以及使用配置，至少掌握一种**

● 编译环境不一样，Sass的安装需要Ruby环境，是在服务端处理的，而Less是需要引入less.js来处理Less代码输出css到浏览器，也可以在开发环节使用Less，然后编译成css文件，直接放到项目中；



● 变量符号不一样，Less是`@`，而Scss是`$`；



● 输出设置，Less没有输出设置，Sass提供4中输出选项：nested, compact, compressed 和 expanded；



● 处理条件语句，Sass支持条件语句，可以使用if{}else{},for{}循环等等。LESS的条件语句使用有些另类，他不是我们常见的关键词if和else if之类，而其实现方式是利用关键词“when”；



● 引用外部文件，文件名如果以下划线_开头的话，Sass会认为该文件是一个引用文件，不会将其编译为css文件，ess引用外部文件和css中的@import没什么差异；



● 工具库的不同，Sass有工具库Compass, 简单说，Sass和Compass的关系有点像Javascript和jQuery的关系,Compass在Sass的基础上，封装了一系列有用的模块和模板，补充强化了Sass的功能。Less有UI组件库Bootstrap,Bootstrap是web前端开发中一个比较有名的前端UI组件库，Bootstrap的样式文件部分源码就是采用Less语法编写。



● PostCSS介绍：

PostCSS 的主要功能只有两个：第一个就是前面提到的把 CSS 解析成 JavaScript 可以操作的 AST，第二个就是调用插件来处理 AST 并得到结果。因此，不能简单的把 PostCSS 归类成 CSS 预处理或后处理工具。PostCSS 所能执行的任务非常多，同时涵盖了传统意义上的预处理和后处理。



● PostCSS使用

PostCSS 一般不单独使用，而是与已有的构建工具进行集成。PostCSS 与主流的构建工具，如 Webpack、Grunt 和 Gulp 都可以进行集成。完成集成之后，选择满足功能需求的 PostCSS 插件并进行配置。现在经常用到的是基于PostCSS的Autoprefixer插件，使用方式可以在官网的插件库进行查询。

## CSS 浏览器兼容性写法

### 样式的初始化

最简单的

```css
*{ 
 margin: 0; 
 padding: 0; 
}
```

Normalize.css 初始化方案

###  浏览器私有属性

私有前缀，比如-webkit-，-moz- ，-ms-，这些就是浏览器的私有属性。

- -moz代表firefox浏览器私有属性
- -ms代表IE浏览器私有属性
- -webkit代表chrome、safari私有属性
- -o代表opera私有属性

对于私有属性的顺序要注意，把标准写法放到最后，兼容性写法放到前面

```css
 -webkit-transform:rotate(-3deg); /*为Chrome/Safari*/ 
 -moz-transform:rotate(-3deg); /*为Firefox*/ 
 -ms-transform:rotate(-3deg); /*为IE*/ 
 -o-transform:rotate(-3deg); /*为Opera*/ 
 transform:rotate(-3deg);
```



#### 自动化插件来处理

Autoprefixer是一款自动管理浏览器前缀的插件，它可以解析CSS文件并且添加浏览器前缀到CSS内容里，使用Can I Use（caniuse网站）的数据来决定哪些前缀是需要的。

## CSS 常用动画

[css常用动画](https://github.com/qappleh/Interview/blob/master/CSS/css常用动画.css)

## 使一个元素隐藏

基本

1. display: none 直接干掉，不占空间
2. visibility： hidden  占空间，视觉上隐藏

技巧：

设置宽高为0，透明度为0， z-index： -1000

## 超链接访问过后 r hover 样式就不出现的问题是什么？如何解决？

被点击访问过的超链接样式不在具有 hover 和 active 了,解决方法是改变 CSS 属性的
排列顺序: L-V-H-A（link,visited,hover,active）

## rgba()和 和 y opacity 的透明效果有什么不同？

rgba()和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度，

而 rgba()只作用于元素的颜色或其背景色。（设置 rgba 透明的元素的子元素不会继承透明效果！）



## S CSS 中 中 k link 和t @import 的区别是：

Link 属于 html 标签，而@import 是 CSS 中提供的

在页面加载的时候，link 会同时被加载，而@import 引用的 CSS 会在页面加载完成后才会加载引用的 CSS

@import 只有在 ie5 以上才可以被识别，而 link 是 html 标签，不存在浏览器兼容性问题
Link 引入样式的权重大于@import 的引用（@import 是将引用的样式导入到当前的页面中）