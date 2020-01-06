# Flex布局

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
