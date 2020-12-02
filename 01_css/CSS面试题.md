## CSS 引入位置

外部样式表，引入一个外部 css 文件
内部样式表，将 css 代码放在 <head> 标签内部
内联样式，将 css 样式直接定义在 HTML 元素内部

## CSS 属性的继承性

CSS 能继承的特性主要是文本方面的继承（比如字体、颜色、字体大小），盒模型相关的属性基本没有继承特性。

## 常用的`@`规则

```css
/*定义字符集*/
@charset "utf-8"
/*导入css文件*/
@import "base.css"
/*自定义字体*/
@font-face {
}
/*声明CSS3 animation动画关键帧*/
@keyframes fadeIn {
}
/*媒体查询*/
@media {
}
```

## CSS 定位规则

### static 普通流定位

默认定位

### float 浮动定位

左浮动和右浮动两个值。

浮动元素会在没有浮动元素的上方展示，效果上看是遮挡住了没有浮动的元素。

有 float 样式的元素是脱离文档流的。他的父元素的高度不能由他撑开。

### relative 相对定位

相对本元素的左上角进行定位。

top、left、botton、right 都可以有值。

经过定位后，位置可能会移动，但是本元素没有脱离文档流，还会占据原来的页面空间。

### absolute 绝对定位

position: absolute

相对于 `祖代`有 relative 定位的元素定位，层级关系最近的元素的左上角进行定位。

如果祖代元素中没有 relative 定位的，就默认相对于 `body`进行定位。

绝对定位是 脱离文档流的。会压在非定位元素上方。

可以设置 z-index 值。

## **雪碧图实现原理：**

CSS 雪碧的基本原理是把你的网站上用到的一些图片整合到一张单独的图片中，从而减少你的网站的 HTTP 请求数量。该图片使用 CSS background 和 background-position 属性渲染，这也就意味着你的标签变得更加复杂了，图片是在 CSS 中定义，而非<img>标签。

## BFC 布局规则

块级格式化上下文，他是一个独立的渲染区域，与外部毫不相干。

### 布局规则：

1. 内部的 Box 会在垂直方向，一个接一个地放置。
2. Box 垂直方向的距离由 margin 决定。属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠
3. 每个元素的 margin box 的左边， 与包含块 border box 的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
4. BFC 的区域不会与 float box 重叠。
5. BFC 就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
6. 计算 BFC 的高度时，浮动元素也参与计算

### **BFC 的作用及原理：**

1.  自适应两栏布局

2.  清除内部浮动

3.  防止垂直 margin 重叠

`BFC`内部的元素和外部的元素绝对不会互相影响，因此， 当`BFC`外部存在浮动时，它不应该影响`BFC`内部 Box 的布局，`BFC`会通过变窄，而不与浮动有重叠。同样的，当`BFC`内部有浮动时，为了不影响外部元素的布局，`BFC`计算高度时会包括浮动的高度。避免 margin 重叠也是这样的一个道理。

## CSS 函数

属性函数：attr()；

背景图片函数： url()

数学函数：calc()、min()、max()、mixmax()、repeat()；

## **PostCSS、Sass、Less 的异同，以及使用配置，至少掌握一种**

● 编译环境不一样，Sass 的安装需要 Ruby 环境，是在服务端处理的，而 Less 是需要引入 less.js 来处理 Less 代码输出 css 到浏览器，也可以在开发环节使用 Less，然后编译成 css 文件，直接放到项目中；

● 变量符号不一样，Less 是`@`，而 Scss 是`$`；

● 输出设置，Less 没有输出设置，Sass 提供 4 中输出选项：nested, compact, compressed 和 expanded；

● 处理条件语句，Sass 支持条件语句，可以使用 if{}else{},for{}循环等等。LESS 的条件语句使用有些另类，他不是我们常见的关键词 if 和 else if 之类，而其实现方式是利用关键词“when”；

● 引用外部文件，文件名如果以下划线\_开头的话，Sass 会认为该文件是一个引用文件，不会将其编译为 css 文件，ess 引用外部文件和 css 中的@import 没什么差异；

● 工具库的不同，Sass 有工具库 Compass, 简单说，Sass 和 Compass 的关系有点像 Javascript 和 jQuery 的关系,Compass 在 Sass 的基础上，封装了一系列有用的模块和模板，补充强化了 Sass 的功能。Less 有 UI 组件库 Bootstrap,Bootstrap 是 web 前端开发中一个比较有名的前端 UI 组件库，Bootstrap 的样式文件部分源码就是采用 Less 语法编写。

● PostCSS 介绍：

PostCSS 的主要功能只有两个：第一个就是前面提到的把 CSS 解析成 JavaScript 可以操作的 AST，第二个就是调用插件来处理 AST 并得到结果。因此，不能简单的把 PostCSS 归类成 CSS 预处理或后处理工具。PostCSS 所能执行的任务非常多，同时涵盖了传统意义上的预处理和后处理。

● PostCSS 使用

PostCSS 一般不单独使用，而是与已有的构建工具进行集成。PostCSS 与主流的构建工具，如 Webpack、Grunt 和 Gulp 都可以进行集成。完成集成之后，选择满足功能需求的 PostCSS 插件并进行配置。现在经常用到的是基于 PostCSS 的 Autoprefixer 插件，使用方式可以在官网的插件库进行查询。

## CSS 浏览器兼容性写法

### 样式的初始化

最简单的

```css
* {
  margin: 0;
  padding: 0;
}
```

Normalize.css 初始化方案

### 浏览器私有属性

私有前缀，比如-webkit-，-moz- ，-ms-，这些就是浏览器的私有属性。

- -moz 代表 firefox 浏览器私有属性
- -ms 代表 IE 浏览器私有属性
- -webkit 代表 chrome、safari 私有属性
- -o 代表 opera 私有属性

对于私有属性的顺序要注意，把标准写法放到最后，兼容性写法放到前面

```css
-webkit-transform: rotate(-3deg); /*为Chrome/Safari*/
-moz-transform: rotate(-3deg); /*为Firefox*/
-ms-transform: rotate(-3deg); /*为IE*/
-o-transform: rotate(-3deg); /*为Opera*/
transform: rotate(-3deg);
```

#### 自动化插件来处理

Autoprefixer 是一款自动管理浏览器前缀的插件，它可以解析 CSS 文件并且添加浏览器前缀到 CSS 内容里，使用 Can I Use（caniuse 网站）的数据来决定哪些前缀是需要的。

## CSS 常用动画

[css 常用动画](https://github.com/qappleh/Interview/blob/master/CSS/css常用动画.css)

## 使一个元素隐藏

基本

1. display: none 直接干掉，不占空间
2. visibility： hidden 占空间，视觉上隐藏

技巧：

设置宽高为 0，透明度为 0， z-index： -1000

## 超链接访问过后 hover 样式就不出现的问题是什么？如何解决？

被点击访问过的超链接样式不在具有 hover 和 active 了,解决方法是改变 CSS 属性的
排列顺序: L-V-H-A（link,visited,hover,active）

## RGBA()和 和 opacity 的透明效果有什么不同？

rgba()和 opacity 都能实现透明效果，但最大的不同是 opacity 作用于元素，以及元素内的所有内容的透明度，

而 rgba()只作用于元素的颜色或其背景色。（设置 rgba 透明的元素的子元素不会继承透明效果！）

## SCSS 中 link 和 @import 的区别是：

Link 属于 html 标签，而@import 是 CSS 中提供的

在页面加载的时候，link 会同时被加载，而@import 引用的 CSS 会在页面加载完成后才会加载引用的 CSS

@import 只有在 ie5 以上才可以被识别，而 link 是 html 标签，不存在浏览器兼容性问题
Link 引入样式的权重大于@import 的引用（@import 是将引用的样式导入到当前的页面中）
