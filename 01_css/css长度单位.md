[css长度](https://www.html.cn/book/css/values/length/index.htm)

[css3新单位vw、vh、vmin、vmax的使用详解](https://blog.csdn.net/ZNYSYS520/article/details/76053961)

## vw、vh、vmin、vmax 的含义

### vh：

相对于视口的高度。视口被均分为100单位的vh

### vw：

视窗宽度的百分比

### vmin：

当前vw和vh中较小的一个值

### vmax：

当前vw和vh中较大的一个值

## vw、vh 与 % 百分比的区别

- **%** 是相对于父元素的大小设定的比率，**vw**、**vh** 是视窗大小决定的。

- **vw**、**vh** 优势在于能够直接获取高度，而用 **%** 在没有设置 **body** 高度的情况下，是无法正确获得可视区域的高度的，所以这是挺不错的优势。

### vmin、vmax 用处

做移动页面开发时，如果使用 **vw**、**wh** 设置字体大小（比如 **5vw**），在竖屏和横屏状态下显示的字体大小是不一样的。

由于 **vmin** 和 **vmax** 是当前较小的 **vw** 和 **vh** 和当前较大的 **vw** 和 **vh**。这里就可以用到 **vmin** 和 **vmax**。使得文字大小在横竖屏下保持一致。

有时为了突出弹出框，或者避免页面元素被点击。我们需要一个覆盖整个可视区域的半透明遮罩，这个使用 **vw**、**vh** 就可以很轻易地实现。

```css
.mask{
    width: 100vw;
        height: 100vh;
        position: fixed;
        top: 0;
        left: 0;
        background: #000000;
        opacity: 0.5;
        display: none;
}
```

