# Grid布局
Flex布局是轴线布局，只能指定项目针对轴线的位置，可以看作是一维布局。
Grid布局则是将容器分割成`行`和`列`,产生单元格，然后指定项目所在的单元格，可以看作是二维布局。

## 基本概念

## 容器属性

`display: grid` 指定一个容器采用网格布局。

`display: inline-grid` 默认情况下设置块级元素，但也可以设置行内元素。

注意： 设为网格布局以后，容器子元素（项目）的`float,display: inlinne-block,display: table-cell, vertical-align,column-*`等设置都失效。

### grid-template-columns，grid-template-rows
```css
.container{
	display: grid;
	grid-template-colums: 100px 100px 100px;
	grid-template-rows: 100px 100px 100px;
}
```
指定了一个三行三列的网格。 列宽和行高都是 100px 。


除了使用绝对单位，也可以使用百分比。

```css
.container{
	display: grid;
	grid-template-column: 33.33% 33.33% 33.33%；
	grid-template-rows: 33.33% 33.33% 33.33%;
}
```

### ==> repeat() 有时候，重读写同样的值，可以使用 repeat()

```css
.container{
	display: grid;
	grid-template-columns: repeat(3, 33.33%);
	grid-template-rows: repeat(3， 33.33%);
}
```
 repeat() 可以接受两个参数，第一个参数是重复的次数，第二个是所要重复的值。 
 ```css
// 重复每种模式也是可以的
	{
		grid-template-cloumns: repeat(2, 100px 20px 80px);
	=>	grid-template-columns: repeat(100px 20px 80px 100px 20px 80px);
	}

 ```

###  auto-fill 关键字
 单元个的大小固定，但是容器的大小不固定。

```css
 .container{
	display: grid;
	grid-template-columns: repeat(auto-fil, 100px);
	// 表示每列宽度是100px， 然后自动填充，直到容器不能放置更多的列。

}
 ```

### fr关键字
	表示比例关系。假设两列的宽度是 `1fr` `2fr` 表示后者是前者的两倍

```css
.container{
	display: grid;
	grid-template-columns: 1fr 1fr; //表示相同宽度的两列。
}

.container{
	display: grid;
	grid-template-columns: 100px 1fr 2fr; // 表示第一列宽度是 100px, 第二列的宽度是第三列的一半
}
```
