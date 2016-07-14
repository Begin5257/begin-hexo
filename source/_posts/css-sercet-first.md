title: CSS揭秘📒
date: 2016-06-24 10:58:36
categories: 归纳整理 #文章文类
tags: [CSS] #文章标签，多于一项时用这种格式
---
### 一些tips
- 使用百分比长度来取代固定长度。
- 需要在较大分辨率下得到固定宽度时，使用 max-width 而不是 width
( max-width 可以适应较小的分辨率，无须媒体查询 )
- 不要忘记为替换元素设计一个宽度，值为100%
- 当图片进行行列式布局时，可以使用弹性盒模型布局( flex )，或 display : inline-box 加上常规的文本折行来实现
- 多列文本时，指定 column-width 列宽，而不是 columm-count 列数。这样就可以在较小的屏幕上自动显示为单列布局
- 合理使用简写

预处理器( Stylus，Sass )
- 变量，mixin，函数，规则嵌套

### 背景与边框
1. 半透明边框
```
.border-container{
        width: 100%;
        height: 600px;
        background: url("http://7xspf8.com2.z0.glb.qiniucdn.com/1467012841.jpg") no-repeat;
    }
    .border-div{
        width: 200px;
        height: 200px;
        margin: auto 50px;
        border: 10px solid rgba(255,255,255,0.5);
        background: #ffffff;
        background-clip: padding-box;
    }
```
线上演示：http://dabblet.com/gist/012289cc14106a1bd7a5

1. 多重边框
```
.div {
background: yellowgreen;
box-shadow: 0 0 0 10px #655,
                0 0 0 15px deeppink,
                0 2px 5px 15px rgba(0,0,0,.6);
}
```
线上演示：http://dabblet.com/gist/525eb8e9cdade71723c1
***若只需要两重边框也可以使用 outline ，可以利用 outline-offset 来控制和元素边缘的间距。( 可为负值 )***

1. 灵活的背景定位
- background-position 
- background-position + background-origin
- calc( )方案 
- calc( )使用时，一定要在内部的 - 和 + 两个运算符侧各加一个空白符，否则会解析错误🙅

```
div {
background: url(http://csssecrets.io/images/code-pirate.svg)
            no-repeat bottom right #58a;
background-position: calc(100% - 20px) calc(100% - 10px);

/* Styling */
max-width: 10em;
min-height: 5em;
padding: 10px;
color: white;
font: 100%/1 sans-serif;
}
```
http://www.w3cplus.com/css3/how-to-use-css3-calc-function.html

1. 边框内圆角

```
div {
outline: .6em solid #655;
box-shadow: 0 0 0 .4em #655; /* todo calculate max of this */

max-width: 10em;
border-radius: .8em;
padding: 1em;
margin: 1em;
background: tan;
font: 100%/1.5 sans-serif;
}
```
线上演示：http://dabblet.com/gist/170fe436f290083cc24c

1. 垂直居中
[http://begin5257.github.io/2016/06/03/vertical-align-div/](http://begin5257.github.io/2016/06/03/vertical-align-div/)