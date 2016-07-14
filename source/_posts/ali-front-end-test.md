title: 2016阿里前端实习生笔试
date: 2016-04-17 12:02:36
categories: 归纳整理 #文章文类
tags: [笔试] #文章标签，多于一项时用这种格式
---

- ~ ~!null //1
~：按位非操作符由一个波浪线（~）表示，执行按位非的结果就是返回数值的反码。
```
~2 === -3; //true
~1 === -2; //true
~0 === -1; //true
~-1 === 0; //true
```
~~: 类似Math.floor()的用法，某些浏览器下比 Math.floor 渲染速度快
[http://rocha.la/JavaScript-bitwise-operators-in-practice](http://rocha.la/JavaScript-bitwise-operators-in-practice)

- 选择合适的选择器选择第二个 p 标签
```
<div>
        <p>p1</p>
        <span>span1</span>
        <p>p2</p>
        <span>span2</span>
</div>
```
  1. div > :nth-last-child(2)
//父元素倒数第二个元素
  2. p:nth-last-child(1)
//错误
  3. p:nth-last-of-type(1)
//仅匹配同种标签的元素，匹配到倒数第一个p
  4. p:nth-of-type(2)
//仅匹配同种标签的元素，匹配到第二个p
  5. p:nth-child(2)
//错误，匹配到父元素下的第二个元素
[http://www.ruanyifeng.com/blog/2009/03/css_selectors.html](http://www.ruanyifeng.com/blog/2009/03/css_selectors.html)


- 原生js相关基础

- 以下属性是否与 IE9 兼容
```
innerHTML/innerText/children/childrennode/classname
```

- 防御XSS注入攻击

- 输入"www.taobao.com"，输出"moc.oab.www"
```
("www.taobao.com").replace("tao","").split("").reverse().join("")
```

- css3动画1s内实现正方形翻转
```
 <style>       
 #loading { 
           width: 100px;
            height: 100px;
            position: absolute;
            animation: circling 1s linear 0s infinite;
        }
        @keyframes circling {
            from {
                transform: rotate(0deg);
            }
            to {
                transform: rotate(360deg);
            }
        }    
</style>
<body>
    <div id="loading"></div>
<body>
```
以前用css3写过一个摇头的(●—●)来着
![](http://7xspf8.com1.z0.glb.clouddn.com/20160125233507_A8NCe.thumb.700_0.png)
[http://begin5257.com/Baymax/](http://begin5257.com/Baymax/)    
[github地址](https://github.com/Begin5257/beginExercise/blob/master/%E5%A4%A7%E7%99%BDcss2.0%2Findex.css)

- 使用css3实现一个长这样的东西![](http://7xspf8.com1.z0.glb.clouddn.com/1163471-12dce4e6d7b63259.png)

主要是星星和边框
[原题](http://pinkyjie.com/2015/03/02/an-interesting-css-interview/) : )
```
 <style>
        a{
            border-radius: 10px;
            text-shadow: 0 1px #eee;
            box-shadow: 0 29px 0 rgba(222, 222, 222, 1) inset,0 0 0 6px #CACACA, 0 0 0        8px #fff, 0px 0px 0px 10px #696969, 0 2px 3px 11px #CBCBCB;

            background: rgba(182, 182, 182, 0.6);
        }
        a:before, a:after {
            font-size: 27px;
            color: #888;
            content: "★";
            text-shadow: 0 1px #fff;
        }
    </style>
```

- 简述一个 js弹窗组件的实现思路
```
触发方式，弹窗内容，消失方式
```

- 设计一个可以监控全站错误并且将错误上报的 js 模块
```
使用 try-catch / window.onerror 捕获异常
阻止常规报错
使用 ajax 将异常发送到某个页面
```
