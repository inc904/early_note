## rem

[(淘宝无限适配)手机端rem布局详解](https://blog.csdn.net/lvyang251314/article/details/82798858)

[简书rem](https://www.jianshu.com/p/d9606faafbaf)



> Equal to the computed value of "font-size" on the root element



`rem`是CSS3新增的相对长度单位，是指相对于**根元素**`html`的`font-size`计算值的大小。简单可理解为屏幕宽度的百分比。



`em`是根据**父级元素**设置大小。



从IE6到Chrome中，默认根元素的`font-size`都是`16px`的。如果想要设置`12px`的字体大小也就是`12px/16px = 0.75rem`。



- 由于`px`是相对固定单位，字号大写直接被定死，无法随着浏览器- 进行缩放。

- `em`和`rem`都是相对单位，`em`是相对于其父元素的`font-size`，页面层级越深，`em`换算越复杂，麻烦。

- `rem`直接相对于根元素`html`，避开层级关系，移动端新型浏览器对其支持较好。

```html
// meta 标签
<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=0"/>
   
```

```js
/**
 * REM自适应
 * designWidth 设计稿实际宽度
 * maxWidth 制作稿的最大宽度
 * */
;(function(designWidth, maxWidth){
    var docEle = document.documentElement;
    //设置viewport
    var meta;
    var viewportContent = "width=device-width,initial-scale=1,maximum-scale=1.0,user-scalable=no,viewport-fit=cover";//viewport-fit=cover用于适配iphoneX
    meta = document.querySelector("meta[name=viewport]");
    if(meta){
        meta.setAttribute("content", viewportContent);
    }else{
        meta = document.createElement("meta");
        meta.setAttribute("name","viewport");
        meta.setAttribute("content", viewportContent);
        if(docEle.firstElementChild){
            docEle.firstElementChild.appendChild(meta);
        }else{
            var div = document.createElement("div");
            div.appendChild(meta);
            document.write(div.innerHTML);
            div = null;
        }
    }

    //创建REM样式
    var styleEle = document.createElement("style");
    if(docEle.firstElementChild){
        docEle.firstElementChild.appendChild(styleEle);
    }else{
        var div = document.createElement("div");
        div.appendChild(styleEle);
        document.write(div.innerHTML);
        div = null;
    }

    //等待viewport设置好后执行refreshRem
    var refreshRem = function(){
        var width = docEle.getBoundingClientRect().width;
        maxWidth = maxWidth || 540;//限制在540的屏幕下，这样100%就跟10rem不一样了
        width > maxWidth && (width = maxWidth);

        var rem = width * 100 / designWidth;
        styleEle.innerHTML = "html{font-size:"+rem+"px !important;}";
    };
    refreshRem();

    //事件监听
    var timeID;
    window.addEventListener("resize", function(){
        clearTimeout(timeID);//防止执行两次
        timeID = setTimeout(refreshRem, 300);
    },false);
    window.addEventListener("pageshow", function(evt){
        //浏览器后退时重新计算
        if(evt.persisted){
            clearTimeout(timeID);
            timeID = setTimeout(refresh, 300);
        }
    },false);

    //事件监听
    var defaultFontSize = "16px";
    if(document.readState === "complete"){
        document.body.style.fontSize = defaultFontSize;
    }else{
        document.addEventListener("DOMContentLoaded", function(evt){
            document.body.style.fontSize = defaultFontSize;
        }, false);
    }
})(720, 750);
```

```css
// 样式重置
/*reset css*/
body,dl,dd,ul,ol,h1,h2,h3,h4,h5,h6,pre,form,input,textarea,p,hr,thead,tbody,tfoot,th,td{margin:0;padding:0;}
ul,ol{list-style:none;}
a{text-decoration:none;}
html{-ms-text-size-adjust:none;-webkit-text-size-adjust:none;text-size-adjust:none;font-size:50px;}
body{line-height:1.5;font-size:16px;}
body,button,input,select,textarea{font-family:'helvetica neue',tahoma,'hiragino sans gb',stheiti,'wenquanyi micro hei',5FAE8F6F96C59ED1,5B8B4F53,sans-serif;}
b,strong{font-weight:bold;}
i,em{font-style:normal;}
table{border-collapse:collapse;border-spacing:0;}
table th,table td{border:1px solid #ddd;padding:5px;}
table th{font-weight:inherit;border-bottom-width:2px;border-bottom-color:#ccc;}
img{border:0 none;width:auto;max-width:100%;vertical-align:top;}
button,input,select,textarea{font-family:inherit;font-size:100%;margin:0;vertical-align:baseline;}
button,html input[type="button"],input[type="reset"],input[type="submit"]{-webkit-appearance:button;cursor:pointer;}
button[disabled],input[disabled]{cursor:default;}
input[type="checkbox"],input[type="radio"]{box-sizing:border-box;padding:0;}
input[type="search"]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box;}
input[type="search"]::-webkit-search-decoration{-webkit-appearance:none;}
@media screen and (-webkit-min-device-pixel-ratio:0){
    input{line-height:normal!important;}
}
select[size],select[multiple],select[size][multiple]{border:1px solid #AAA;padding:0;}
article,aside,details,figcaption,figure,footer,header,hgroup,main,nav,section,summary{display:block;}
audio,canvas,video,progress{display:inline-block;}
```

### tuyou

```js
//rem适配
    function resize() {
            var clientWidth = document.documentElement.clientWidth;
            document.documentElement.style.fontSize = 100 * (clientWidth / 320) + 'px';
    };
    resize();
    window.addEventListener('resize', resize);
```

