# Flex布局



## 什么是Flex布局

	Flex布局：“弹性布局”。任何元素都可以使用 flex 布局，行内元素也可以，Webkit内核的浏览器，必须加上 `-webkit` 前缀.
	设置 Flex 布局以后，子元素的 float ， clear ，vertical-align 属性都会失效。

## 基本概念

Flex 容器，他的子成员自动成为容器成员，称为‘项目成员’。

容器默认存在连两根轴，主轴和交叉轴，

## 容器的属性

### 六大属性

1. flex-direction：主轴方向，即项目的排列方向

   ```css
   .box{
   	flex-direction: row | row-reverse | column | column-reverse;
   }
   ```

2. flex-wrap: 项目在一条轴线上如何换行
   取值： nowrap | wrap | wrap-reverse

3. flex-flow： 是flex-direction 和 flex-wrap 的简写形式
   `{ flex-flow: flex-direction flex-wrap; }`

4. justify-content: 项目在主轴上的对齐方式
   取值： flex-start | flex-end | center | space-between | space-around

  左对齐（默认） | 右对齐 | 水平居中 |  间隔平铺（两端顶头） | 间隔平铺（两端留间隔） 

5. align-items： 项目在交叉轴上如何对齐

  取值： flex-start | flex-end | center | baseline | stretch 

  交叉轴起点对齐 | 交叉轴 终点对齐 | 交叉轴 中点 对齐 | 项目的第一行文字基线对齐 | 高度占满容器（默认）

6. align-content 定义多根轴线的对齐方式，如果项目只有一根轴线，此属性无效
   取值： flex-start | flex-end | center | space-between | space-around | stretch;

## 项目的属性 

### 六大属性

1. order 项目的排列顺序，数值越小，排列越靠前，默认值是 0 

2. flex-grow 项目的放大比例，默认为 0 ，即使有剩空间也不放大

3. flex-shrink 项目的缩小比例。
   默认为 1，即空间不足，该项目缩小 如果所有项目的 flex-shrink 都为1，当空间不足时，都将等比缩小，

   如果一个项目的 felx-shrink属性为0，其他项目为1， 则空间不足是，前者不缩小， 其他缩小

4. flex-basis 定义项目在分配多余空间之前，项目占据主轴空间，浏览器根据在这个属性计算主轴是否有多余空间，默认值 auto ，即 项目本来的大小
   取值：  <length> | auto

5. flex flex-grow flex-shrink flex-basis 的简写

6. align-self 允许单个项目有与其他项目不一样的对齐方式，可以覆盖 `align-item`属性，默认值 `auto`，表示继承父元素的`align-item`属性
   取值： auto | flex-start | flex-end | center | baseline | stretch;



## 容器的属性

- `justify-content` 项目在主轴上的对齐方式。
    取值：`flex-start 靠左 | flex-end 靠右 | center 居中 | space-between 两端顶边，间隔相等 | space-around 两端留空，间隔相等 `

- `flex-wrap` 在轴线上的换行方式。
    取值 `wrap`|`no-wrap`|`wrap-reverse`

- `align-items` 项目在交叉轴上的对齐方式。
    取值：`flex-start 靠顶 | flex-end 靠底 | center 居中 | baseline 文字基线对齐 | stretch 充满交叉轴高度` 

- `flex-direction` 主轴方向。
    取值水平方向：
  
  - `row` 水平方向，从左至右。
  - `row-reverse` 水平方向，从由至左。
    取值垂直方向：
  - `column`  垂直方向，从上到下。
  - `column-reverse` 垂直方向，从下往上。

- `flex-flow`
    是`flex-direction` 和`flex-wrap`的简写形式。
    取值：`flex-direction` || `flex-wrap`

- `align-content` 定义了多根轴线的对齐方式（发生换行的情况），如果只有一根轴线，该属性不起作用。
  取值： `flex-start | flex-end | center | space-between | space-around | stretch;`

## 项目的属性

- `align-self` 允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。

- `order` 项目排序。数值越小，排序靠前。默认为0。

- `flex-grow` 项目放大比例。默认为0，大的值将占据剩余空间。

- `flex-shrink` 项目缩小比例。默认为1，即如果空间不足，该项目将会缩小。

- `flex-basis`

- `flex` `flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为0 1 auto。后两个属性可选。
