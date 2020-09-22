[sass中文网](https://www.sass.hk/guide/)

```scss
/* 变量声明： */
/* 变量名中 中划线 和 下划线都可以 */
$bg-color: #f00;
.box{
    $widht: 100px
    /*变量 引用*/
     // $width 定义在当前的{} 规则块中，所以只能在当前的规则块中使用    
    width: $width;
    /* $bg-color 定义在外面，所以这个样式表任何地方都可以引用 */
    background-color: $bg-color;
}

/* 嵌套规则 */
#content {
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  #content aside { background-color: #EEE }
}

/*  父选择器的标识 & */
article a {
  color: blue;
    /* 等价于 article a:hover  */
  &:hover { color: red }
}
```

