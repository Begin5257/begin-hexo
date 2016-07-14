title: CSS布局(box-sizing,column,flex,inline-box布局)
date: 2016-04-28 21:01:36
categories: 归纳整理 #文章文类
tags: [CSS] #文章标签，多于一项时用这种格式
---

- 布局除了 position，float之外，还可以使用 inline-box
  1. vertical-align 属性会影响到 inline-block元素，你可能会把它的值设置为top。
  2. 你需要设置每一列的宽度
  3. 如果HTML源代码中元素之间有空格，那么列与列之间会产生空隙
![](http://7xspf8.com1.z0.glb.clouddn.com/inline-box20160428182717.png)
```
nav {
    display: inline-block;
    vertical-align: top;
    width: 25%;
    border: 1px solid yellowgreen;
}
.column {
    display: inline-block;
    vertical-align: top;
    width: 74%;
    border: 1px solid #66BAB7;
}
```
[更多display](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
- 清除浮动
![](http://7xspf8.com1.z0.glb.clouddn.com/before-20160428182033.png)
```
.box {
    float: left;
    width: 200px;
    height: 100px;
    margin: 1em;
    border: 1px solid #66BAB7;
}
.after-box {
    clear: left;/*left和both都可以*/
    border: 1px solid yellowgreen;
}
```
![](http://7xspf8.com1.z0.glb.clouddn.com/after-20160428182021.png)
[http://zh.learnlayout.com/clearfix.html](http://zh.learnlayout.com/clearfix.html)
[清除浮动水很深](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)

- column
多列布局
```
.three-column{
    border: 1px solid #66BAB7;
    padding: 1em;
    -webkit-column-count: 3;
    column-count: 3;
    -webkit-column-gap: 1em;
    column-gap: 1em;
}
```
![大概这么个效果](http://7xspf8.com1.z0.glb.clouddn.com/column-20160428194453.png)

- box-sizing 
当你设置一个元素为 box-sizing: border-box 时，此元素的内边距和边框不再会增加它的宽度。
```
/*此时内边距和边框都不会增加它的宽度*/
.simple {
    width: 500px;
    margin: 20px auto;
    border: 1px solid blue;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}
.fancy {
    width: 500px;
    margin: 20px auto;
    padding: 50px;
    border: 10px solid blue;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}
```
![](http://7xspf8.com1.z0.glb.clouddn.com/box-sizing-20160428195136.png)

- flex布局
 1. 简单的 flex 布局
![](http://7xspf8.com1.z0.glb.clouddn.com/easy-flex-20160428195502.png)
```
.container {
    display: -webkit-flex;
    display: flex;
    background: lightblue;
}
nav {
    width: 200px;
    background: #66BAB7;
}
.flex-column {
    flex: 1;
    -webkit-flex: 1;
    background: yellowgreen;
}
```
 2. 复杂的 flex 布局
![](http://7xspf8.com1.z0.glb.clouddn.com/hard-flex-20160428195531.png)
```
.container {
    display: flex;
    display: -webkit-flex;
}
.first {
    flex: initial;
    -webkit-flex: initial;
    width: 200px;
    min-width: 100px;
    background: red;
}
.none {
    flex: none;
    -webkit-flex: none;
    width: 200px;
    background: yellow;
}
.flex1 {
    flex: 1;
    -webkit-flex: 1;
    background: yellowgreen;
}
.flex2 {
    flex: 2;
    -webkit-flex: 2;
    background: #66BAB7;
}
```
 3. 居中 flex 布局
![](http://7xspf8.com1.z0.glb.clouddn.com/vertical-flex-20160428195552.png)
```
.vertical-container {
    height: 500px;
    display: -webkit-flex;
    display: flex;
    -webkit-align-items: center;
    align-items: center;
    -webkit-justify-content: center;
    justify-content: center;
}
.div {
    width: 200px;
    height: 200px;
    border: 10px solid #66BAB7;
}
```
安利：[http://zh.learnlayout.com/toc.html](http://zh.learnlayout.com/toc.html)
