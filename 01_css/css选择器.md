`+` 直接相邻兄弟选择器
`~` 所有兄弟选择器
`>` 后代选择器

## CSS 选择器

- 通用选择器： \* {}
- id 选择器：#header {}
- class 选择器：.header {}
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
