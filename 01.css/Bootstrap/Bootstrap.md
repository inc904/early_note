## 目录结构
- css目录
带min字样的是编译压缩后的压缩版，可以用于生产部署环境，
不带min的可以用于开发调试版本，
带map字样的是css地图查询文件，方便查询精确的样式位置。

- js目录	

## 布局系统
### 布局介绍

- 对于容器布局，bt4.x 提供了`.container`和`.container-fluid`两种；
- 这两种方式是启用布局栅格系统的最基本要素；
- `.container`是固体自适应的方式，`.container-fluid`是流体100%自适应方式；
- 容器布局可以嵌套，但一般不推荐且很少用到；
- 自适应对应的相应方式如下 media：
```css
// small devices (landscape phones, 576px and up)
@media (min-width: 576px){ ... }

// medium devices (talebs, 768px and up)
@media (min-width: 768px){ ... }

// large devices( desktops 992px and up)
@media ( min-width: 992px ){ ... }

// extra large devices( large desktops, 1200px and up )
@media(min-width: 1200px){ ... }
```
- 从响应式的 media 可以看出吗，Bt4.x 是以移动端为优先的。

### 栅格系统

- Bt4.x 的栅格系统是一个以移动为优先的网格系统；

- 基于 12 列的布局，5种响应式尺寸（面向不用屏幕设备）

- 完成使用 `Flexbox` 流式布局构建的，完全支持响应式标准；

- 具体采用 div 容器的行、列和对齐内用来构建响应式布局；

- `.row` 表示一行，`.col-*`表示一列 

### 栅格对齐

- 对于栅格系统中的行（row），可以对齐进行垂直对齐操作

| 居顶（默认） | .align-items-start  |
| ------------ | ------------------- |
| 居中         | .align-items-center |
| 居底         | .align-items-end    |

- 对于栅格系统中的列（col-）,进行`垂直对齐`操作

| 居顶（默认） | .align-self-start  |
| ----------- | ------------------ |
| 居中         | .align-self-center |
| 居底         | .align-self-end    |



- 对于不足以100%填充的行，实现`水平对齐`方式

| 居顶（默认） | .align-self-start   |
| ------------ | ------------------- |
| 居中         | .align-self-center  |
| 居底         | .align-self-end     |
| 间隔相等分散 | .align-self-around  |
| 两端对齐分散 | .align-self-between |

### 栅格排列和偏移

#### 排列

- 使用`.order-N`进行排序，N最大值是12

- 可以使用`.order-first` ,`.order-last`强行设置第一行和最后一行

#### 偏移

- 使用`.offset-N`或者`.offset-*-N`来设置偏移

- 使用`.ml-N`或者`.mr-N`来微调距离，使用`.ml-auto`或者`.mr-auto`来左右对齐

### 内容排版

#### 标题类

- `h1-h6`标签和`.h1~.h6`类名

- 在标题内容中嵌套`small`标签，生成副标题，类`text-muted`可以设置副标题的字体颜色为近灰色。

- `display-1~4` 设置标题，更大更醒目

#### 文本类

- `.lead`表强调

#### 列表类
- `.list-unstyle` 将列表初始化，去掉小圆点
- `list-inline`和`list-inline-item`结合实现多列并排排列列表
- `dl dt dd` 实现水平描述，`.text-truncate`可以省略溢出

### 代码与图文

#### 代码

#### 图文
