title: Tmall开发
date: 2016-02-09 15:39:36
categories: 开发总结 #文章文类
tags: [JavaScript] #文章标签，多于一项时用这种格式
---
1.29
假期无聊，打算来临摹一个大型网站，练习一下js和css。
效果如下：![](http://7xspf8.com2.z0.glb.qiniucdn.com/20160129233346_LxKEh.thumb.700_0.png)
源码地址：https://github.com/Begin5257/Tmall.git
喜欢天猫的黑红，所以就天猫啦。
js全部基于原生js和jQuery。 

一些需要注意的点：
1、nav栏鼠标滑过出现div
用jQuery实现，需要注意的是上面链接的背景颜色也要随着改变。 
2、小三角鼠标滑过变成倒三角
小三角是这样的，将三边设成transparent即可得到
border-color:#bbbbbb transparent transparent
倒三角是这样：
border-color:transparent transparent #bbbbbb
3、出现的div上面有小尖头
利用b标签的border，原理同上 
4、点击切换大图
利用原生js实现 
5、图片轮播
利用原生js，复习了setTimeout的使用方法。

今天的效果是这样的～

1.30
今天主要解决了下滑固定div出现nav的效果。
效果如下：![](http://7xspf8.com2.z0.glb.qiniucdn.com/20160130231434_WTnSh.thumb.700_0.png)

啊，鼠标滚轮真是个神奇的事件。
是难得一见的Firefox派和其他派系(一般都是IE和其他2333)
 
•Firefox 鼠标滚轮向上滚动是-3，向下滚动是3
•IE 鼠标滚轮向上滚动是120，向下滚动是-120
•Safari 鼠标滚轮向上滚动是360，向下滚动是-360
•Opera 鼠标滚轮向上滚动是120，向下滚动是-120
•Chrome 鼠标滚轮向上滚动是120，向下滚动是-120
 
反正JS可以根据正负判断向上滚还是向下滚，那么就好说了。
贴个源码：
//下滑鼠标出现隐藏nav,上滑隐藏
```
function showNav(){
    var div = document.getElementById('main-content');
    var img=document.getElementById("scroll-img");
    var nav=document.getElementById("slide-nav");
    //addEventListener兼容IE
    if (div.addEventListener) {
        div.addEventListener('DOMMouseScroll', function(event) {
            event = event || window.event;
            //JavaScript获取鼠标滚轮值，这里的值只有“1”和“-1”两种情况
            if(event.wheelDelta<0) {
                nav.style.display = "inline";
            }
        }, false);
    }
    if (img.addEventListener) {
        img.addEventListener('DOMMouseScroll', function(event) {
            event = event || window.event;
            if(event.wheelDelta>0){
                nav.style.display="none";
            }
        }, false);
    }
    
    div.onmousewheel = function(event) {
        event = event || window.event;
        if(event.wheelDelta<0){
            nav.style.display="inline";
        }
    };
    img.onmousewheel = function(event) {
        event = event || window.event;
        if(event.wheelDelta>0){
            nav.style.display="none";
        }
    }
}
```
