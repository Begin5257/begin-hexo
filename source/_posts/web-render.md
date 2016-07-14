title: 浏览器渲染机制
date: 2016-04-02 21:01:36
categories: 归纳整理 #文章文类
tags: [浏览器渲染机制] #文章标签，多于一项时用这种格式
---
#### 一.加载

浏览器的五个常驻线程：

1. 浏览器 GUI 渲染线程

2. javascript 引擎线程

3. 浏览器定时器触发线程( setTimeout,setInterval )

4. 浏览器事件触发线程

5. 浏览器 http 异步请求

当js引擎线程（第二个）进行时，会挂起其他一切线程，这个时候3、4、5这三类线程也会产生不同的异步事件，由于 javascript引擎线程为单线程，所以代码都是先压到队列，采用先进先出的方式运行，事件处理函数，timer函数也会压在队列中，不断的从队头取出事件，这就叫：javascript-event-loop。简单点说应该是当在进行第二线程的时候，1，3，4，5都会挂起，比如这时候触发click事件，即使先前JS已经加载完成，click事件会压在队列里，这里也要先完成第二线程才会执行click事件。

加载顺序：[http://www.cnblogs.com/web-easy/p/5067680.html](http://www.cnblogs.com/web-easy/p/5067680.html)

#### 二、渲染

渲染引擎的职责，就是负责把从服务器返回HTML，XML或者images等资源渲染并展现给用户。

常用的渲染引擎有：webkit ( chrome, safari, opera ) 和 gecko ( firefox )。

![](http://7xspf8.com2.z0.glb.qiniucdn.com/30174422-85c05a2dac024b3d8aca392015807f7d.png)

基本的渲染过程：

1. 渲染引擎首先会解析 HTML 文档，转化为 DOM 树。

2. 解析 CSS 的样式，渲染出另外一棵用于渲染 DOM 树的 render-tree ，render-tree 中包含有 css 中的颜色，属性等。

3. 对 render-tree 中的每个节点进行布局，确定其在屏幕上的位置。

4. 遍历渲染树，将每一个节点绘制出来。



webkit 的渲染流程：

![](http://7xspf8.com2.z0.glb.qiniucdn.com/30174613-aea0f7a683574d87a7fa049dc52f5ae3.png)

gecko 的渲染流程：

![](http://7xspf8.com2.z0.glb.qiniucdn.com/30174629-d2e8eba07c05420dbc3a049a0de099a7.jpg)

通过上图可以看出，webkit 与 gecko 最大的区别就是渲染样式的时间。

webkit 中，解析 HTML 与 CSS 样式是同时发生的。

而 gecko 中 HTML 解析出 content-sink ( DOM树搭建前的 pre-model ) 之后，按照 pre-model 来解析样式。

[关于 content-sink](http://onwebdev.blogspot.com/2010/05/content-sink-and-dom-construction.html)



样式计算优先级：

1. 浏览器默认样式

2. 用户个性化浏览器设置

3. HTML 开发者定义的一般样式

4. 开发者定义的 !important 样式

5. 用户个性浏览器设置的 !important 样式



更详细的：

通用选择器（*）>元素(类型)选择器>类选择器>属性选择器>伪类>ID 选择器>内联样式

count 1 if the declaration is from is a 'style' attribute rather than a rule with a selector, 0 otherwise (= a)

count the number of ID attributes in the selector (= b)

count the number of other attributes and pseudo-classes in the selector (= c)

count the number of element names and pseudo-elements in the selector (= d)

举例说明

```

*            {}  /* a=0 b=0 c=0 d=0 -> specificity = 0,0,0,0 */

li            {}  /* a=0 b=0 c=0 d=1 -> specificity = 0,0,0,1 */

li:first-line {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */

ul li        {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */

ul ol+li      {}  /* a=0 b=0 c=0 d=3 -> specificity = 0,0,0,3 */

h1 + *[rel=up]{}  /* a=0 b=0 c=1 d=1 -> specificity = 0,0,1,1 */

ul ol li.red  {}  /* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 */

li.red.level  {}  /* a=0 b=0 c=2 d=1 -> specificity = 0,0,2,1 */

#x34y        {}  /* a=0 b=1 c=0 d=0 -> specificity = 0,1,0,0 */

style=""          /* a=1 b=0 c=0 d=0 -> specificity = 1,0,0,0 */

```

> 上面确定了renderer的样式规则后，然后就是重要的显示因素布局了。当renderer构造出来并添加到render树上之后，它并没有位置跟大小信息，为它确定这些信息的过程，我们就称之为布局。HTML采用了一种流式布局的布局模型，从上到下，从左到右顺序布局，布局的起点是从render树的根节点开始的，对应dom树的document节点，其初始位置为0,0,详细的布局过程为： 每个renderer的宽度由父节点的renderer确定。 父节点遍历子节点，确定子节点的位置（x,y)，调用子节点的layout方法确定其高度。 父节点根据子节点的height,margin,padding确定自身的自身的高度。

> 为了避免因为局部小范围的DOM修改或者样式改变引起整个页面整体的布局重新构造，浏览器采用了一种dirty bit system的技术，使其尽可能的只改变元素本身或者包含的子元素的布局。当然有些情况无可避免的要重新构造整个页面的布局，如适合于整体的样式的改变影响了所有renderer，如body{font-size:111px} 字体大小发生了改变，还有一种情况就是浏览器窗口进行了调整，resize。

参考：

[https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)

[http://www.cnblogs.com/xugang/archive/2010/09/24/1833760.html](http://www.cnblogs.com/xugang/archive/2010/09/24/1833760.html)
