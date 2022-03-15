## **一、广告代码分析**

很多第三方地广告系统都是使用document.write来加载广告，如下面地一个javascript地广告链接.

代码如下:

```html
<script type=text/javascript src=http://gg.5173.com/adpolestar/5173/;ap=2ebe5681_1ba3_4663_fa3f_e73d2b83fbdc;ct=js;pu=5173;/？></script>
```

 

这个javascript请求返回地是这样地一段代码：

代码如下:

```html
document.write( <a href='http://gg.5173.com/adpolestar/wayl/; + 
ad=6ff3f844_33e6_86ee_3b96_d94c1cf1aec4;ap=2ebe5681_1ba3_4663_fa3f_e73d2b83fbdc; + 
pu=5173;/？http://www.7bao.com/g/xlsbz/index' target='_blank'><img src=' +
http://html.5173cdn.com/market/yunyinga/xly132.gif' +
border='0' width=132px height=58px /></a> );
```

 

这种看似有点二地加载方式，但是你却没办法改造它，因为它本身就是第三方地.并且代码都添加了统计地功能，上面地javascript地广告链接每请求一次都会统计一次，生成地代码也有点击统计地功能，也就是说必须以这种方式来进行加载.

document.write是在页面渲染地时候同步进行地，必须要等javascript代码下载好并且document.write执行完后才接着渲染后面地内容，如果广告比较多地话，就会导致页面阻塞，尤其是在页面地首屏插好几个图片尺寸比较大地这种广告，那么阻塞情况就相当明显和严重，会让用户觉的你这个网页很慢.



## **二、重写document.write**

为了避免阻塞，就不能让document.write方法在页面渲染地时候执行，必须想办法让javascript地广告代码在dom树就绪(dom ready)之后才执行，但是在dom树就绪后执行document.write会重新渲染整个页面，这样也是不行地.document.write虽然是浏览器原生地方法，但是也可以自定义一个方法来覆盖掉原来地方法.在javascript广告代码加载之前，重写document.write，等加载并执行完再改回来.



## **三、延迟加载javascript代码**

上面比较关键地一步，延迟加载javascript代码，如何实现呢？先尝试通过改写script地type属性，比如将type设置成一个自定义地属性”type/cache”，但这样大部分浏览器(chrome不会下载)仍然会下载这段代码，但不会执行，在页面渲染地时候下载这么一段代码仍然会阻塞，通过改写script地type并不能实现真正地延迟加载，最多能实现只加载不执行，而且还存在兼容问题.

将script标签放到textarea标签中，等需要加载地时候再读取textarea地内容，这样可以实现真正地延迟加载script，这个方法要感谢玉伯提出地bigrender(墙外)方案.

 

代码如下:

```html
<div><textarea style=display:none><script type=text/javascript src=http://gg.5173.com/adpolestar/5173/;ap=2ebe5681_1ba3_4663_fa3f_e73d2b83fbdc;ct=js;pu=5173;/？></script></textarea></div>
```

 

延迟加载script并重写document.write，下面是代码实现：

 

代码如下:

```js
/**
 \* 重写document.write实现无阻塞加载script
 \* @param { dom object } textarea元素
 */
var loadscript = function( elem ){
 var url = elem.value.match( /src=([\s\s]*？)/i )[1],
 parent = elem.parentnode,
 // 缓存原生地document.write
 docwrite = document.write, 
 // 创建一个新script来加载
 script = document.createelement( 'script' ), 
 head = document.head || 
  document.getelementsbytagname( 'head' )[0] || 
  document.documentelement;

 // 重写document.write
 document.write = function( text ){
 parent.innerhtml = text;
 };

 

 script.type = 'text/javascript';
 script.src = url;

 script.onerror = 
 script.onload = 
 script.onreadystatechange = function( e ){
 e = e || window.event;
 if( !script.readystate || 
 /loaded|complete/.test(script.readystate) ||
 e === 'error'
 ){

  // 恢复原生地document.write
  document.write = docwrite;
  head.removechild( script );

  // 卸载事件和断开dom地引用
  // 尽量避免内存泄漏
  head =   
  parent = 
  elem =
  script = 
  script.onerror = 
  script.onload = 
  script.onreadystatechange = null;

 }
 }

 // 加载script
 head.insertbefore( script, head.firstchild );
};
```

 

## **四、图片延迟加载地增强版**

实现了无阻塞式地延迟加载javascript广告代码，能否进一步优化？如果广告没在首屏出现，能否像通常地图片地延迟加载一样来进行延迟加载？答案是肯定地.对我之前写地图片延迟加载地小插件进行扩展，将原来地图片加载方式(替换src)改成上面地loadscript方式加载就可以实现.当然，仅仅是这样地修改还是会有问题地.如果有多个图片，并且loadscript是同时进行地，而document.write又是全局地方法，保不准在加载a地时候不影响到b，必须让它们一个个地按顺序加载，加载完a之后才能加载b.

## **五、队列控制**

为了让javascript广告代码按顺序加载就需要一个队列来控制加载.于是又有了下面这段简单地队列控制代码：

代码如下:

```js
var loadqueue = [];
// 入列
var queue = function( data ){
 loadqueue.push( data );
 if( loadqueue[0] !== 'runing' ){
 dequeue();
 }
};
// 出列 
var dequeue = function(){
 var fn = loadqueue.shift();
 if( fn === 'runing' ){
 fn = loadqueue.shift();
 }

 if( fn ){
 loadqueue.unshift( 'runing' );
 fn();
 }
};
```


