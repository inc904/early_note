# markdown语法 [官网](http://www.markdown.cn/)

## 这是标题
“#加空格” 是标题，通常可以设置六级标题。
### 内容下 空格是换行

----
## 列表
**无序列表：**使用“ - + * ”任何一种加空格都可以
- 列表内容

+ 列表内容

* 列表内容

**有序列表：**数字加点加空格

1. 有序1
2. 有序2
3. 有序3

**列表嵌套**上一级和下一级之间敲三个空格
```
- 一级无序列表
123- 二级无序列表
   - 二级无序列表
   - 二级无序列表

```
- 一级无序列表
   - 二级无序列表
   - 二级无序列表
   - 二级无序列表


## 字体部分
要**加粗**的字体：用两个“**”包起来。

要*倾斜*的字体：用一个“*”包起来

要 ***倾斜和加粗***的字体：用三个“***”包起来

要加~~删除线~~``的字体：用两个“~~”包起来


## 引用
引用的文字前加 “ > ” 包裹，可以逐级嵌套
> 库克：
>> stay  foolish, stay hungry!

## 分割线
三个或者三个以上的 “-”“+”“*”都可以

减号分割

----

减号分割线下一行紧接文字（加粗加大文字，线会比较细）
---

加号分割（失效？）

++++

星号分割
****

## 图片
语法：`  ![图片的alt](图片的地址 "图片的title")  `

图片的alt就是现实在图片下面的文字，相当于对图片内容的解释。

图片的title是图片的标题，当鼠标移动到图片上显示的内容，title可加可不加

示例：

`![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/
u=702257389,1274025419&fm=27&gp=0.jpg "区块链")`

![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/
u=702257389,1274025419&fm=27&gp=0.jpg "区块链")

## 超链接

语法： `[超链接名](超链接地址 "超链接title")  ` 

title可加可不加

示例：`[百度](http://baidu.com)`

[百度](http://baidu.com)

## 表格
语法：

```

表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

```
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

第二行分割表头和内容。
- 有一个就行，为了对齐，多加了几个
文字默认居左
- 两边加：表示文字居中
- 右边加：表示文字居右
注：原生的语法两边都要用 | 包起来。此处省略

## 代码
### oem键的使用:
英文下 单击oem： ` （反引号）

英文下shift + oem：~

中文下单机oem：·

中文下shift + oem：~

中英文下shift + oem 都是 ~

三个英文下单机oem包裹，是代码块
```
**本来是加粗**
```
### 代码语法
单行代码：代码用一个引号包裹起来

多行代码用三个反引号包裹
```
`asdasdasdasd`
```
`asdasdasdasd`
```
function fun(){
	console.log("乾坤未定")
}
```
## 流程图
(不会用)
```
flow
st=>start: 开始
op=>operation: My Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->op
&
```
flow
st=>start: 开始
op=>operation: My Operation
cond=>condition: Yes or No?
e=>end
st->op->cond
cond(yes)->e
cond(no)->op
&

## 支持兼容HTML代码
谷歌预览好像还有隔行变色功能

<table>
    <tr>
        <td>Foo</td>
		<td>Foo</td>
        <td>Foo</td>
    </tr>
	<tr>
	    <td>Foo</td>
		<td>Foo</td>
        <td>Foo</td>
	</tr>
	<tr>
	    <td>Foo</td>
		<td>Foo</td>
	    <td>Foo</td>
	</tr>
</table>

<span>span标签</span>

*在html区块中，md格式的语法不在生效*
