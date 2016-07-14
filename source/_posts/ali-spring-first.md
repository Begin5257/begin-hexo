title: 阿里面试--一面小结
date: 2016-05-19 12:02:36
categories: 归纳整理 #文章文类
tags: [面试] #文章标签，多于一项时用这种格式
---
(=@__@=)前一天晚上因为甲方的逼迫通宵改项目，第二天阿里面试
状态很糟糕，刚刚回学校考完试啦，现在来记录一下面试的过程🍉
***
一面
(和蔼的) 介绍一下你的学习经历~
(懵逼的) HTML5，CSS3，JavaScript，PHP+MySQL，nodeJS，Angular.JS，Vue.JS，最近在学react
(超级喜(猥)悦(琐)) 你知不知道面试的时候提Angular和Vue是很危险的呀~
![](http://7xspf8.com1.z0.glb.clouddn.com/2.pic.jpg)
***
(开心的) 那我们来几个最最最基本的问题吧
(终于进入正题了啊) 嗯嗯！
(正经的) 来讲讲跨域
(依旧懵逼的)
最普通的有CORS(但是当时懵逼的我说成了CSRF，大写的囧)，服务端允许跨域。这个会有简单请求和复杂请求两种。简单请求就是 GET请求( 除了Content-Type是json格式 )，复杂请求就是除此之外的请求。 区别就是复杂请求在发送正式请求之前会提前发送一个OPTIONS请求，服务端如果允许了这个OPTIONS请求，那就会接着去发正式请求。
然后就是 jsonp ，通过带有src属性的标签就可以跨域访问。在标签的回调函数里添加对请求到的数据的处理方法就可以啦~
(严肃的) 别的呢？？
(想了想) 还有iframe
(恍然大悟) 对了，前些天做项目的时候用到了h5的postMessage，后台那边在官网添加首页图片预览。本地调试时在我的代码里引用一个带有他域名的js文件，就可以实现了后台添加图片的实时预览。
(继续问) 还有呢？？
(懵逼的) ？？
(告诉我) 还有domain和flash然后balabala(我现在具体想不来了其实= =)

***
(笑的超开心)来谈谈(你刚刚提到的)CSRF
![](http://7xspf8.com1.z0.glb.clouddn.com/2.pic.jpg)
(反应过来并假装自己刚刚什么都没有说然后一本正经的说)
跨站伪造请求嘛，典型的可以通过盗取cookie来得到用户的各种权限。
(微笑) 只有这样？
(继续正经) 那其实可以插入js的话也就等同于可以做任何事情了。其实有时候和XSS会有点像。
(正经脸) CSRF和XSS是完全不同的。
(懵逼) (⊙o⊙)
(正经讲解脸) **跨站请求伪造**是一种挟制用户在当前已登录的Web应用程序上执行非本意的操作的攻击方法。跟[跨网站脚本](https://zh.wikipedia.org/wiki/%E8%B7%A8%E7%B6%B2%E7%AB%99%E6%8C%87%E4%BB%A4%E7%A2%BC)（XSS）相比，**XSS** 利用的是用户对指定网站的信任，CSRF 利用的是网站对用户网页浏览器的信任。攻击者并不能通过CSRF攻击来直接获取用户的账户控制权，也不能直接窃取用户的任何信息。他们能做到的，是**欺骗用户浏览器，让其以用户的名义执行操作**。
(开心的) 原理告诉你了，来，猜猜看怎么防御
(懵逼的) 可不可以直接屏蔽掉所有的外来js 啊？？
(严肃的) 不是这个问题
(想了想) 应该是类似浏览器同源策略的方法吧，通过限制特点的域名下的js才能对网站进行访问
(正经脸继续解释) 检查Referer字段，HTTP头中有一个Referer字段，这个字段用以标明请求来源于哪个地址。在处理敏感数据请求时，通常来说，Referer字段应和请求的地址位于同一域名下。
还有呢？？
(此时已经完全懵) 想不出来了
(正经脸) Web Authentication知道吗？
(正经脸) 嗯嗯，前些天做项目时有遇到。在用户登录后再向服务端发送请求时都会要求携带token，只有token正确服务端才会返回数据。
(好奇脸) 那token就一定安全了嘛？
(懵逼) 似乎不吧，万一cookie被盗用😳
(嫌弃脸) 现在的网站有那么不安全吗，其实 token就已经完全可以防御CSRF了
那想想在阿里CSRF防御可以用在哪些地方？
(懵逼脸) 支付的过程吧
(我觉得他已经进入讲解状态了科科) 就拿支付宝说，如果盗用了用户权限，随意修改一下转账的account和转账的money，嗯，钱就没有了。

此时我的心情：
![](http://7xspf8.com1.z0.glb.clouddn.com/2.pic.jpg)
***
(愉悦脸) 来来我们先来谈一下这个你刚刚提到的angular，它是mvvm结构，那它是怎么实现数据双向绑定的？
(完全懵逼) 不是很清楚
(超爽快) 来，手机给你，两分钟，自己查完给我讲
--------------***认真百度的分割线***-------------
(正经脸) Angular的数据绑定主要是通过中间的ViewModel层($scope)来实现的。引入了专门的ViewModel（视图模型）来实现View和Model的粘合，让View和Model的进一步分离。
--------------***认真装逼的分割线***-------------
[http://imweb.io/topic/55c05482193684376cd08b53](http://imweb.io/topic/55c05482193684376cd08b53)
[https://www.zhihu.com/question/23275373](https://www.zhihu.com/question/23275373)
[http://www.alloyteam.com/2015/06/mvvm-xue-xi-vue-shi-jian-xiao-jie/](http://www.alloyteam.com/2015/06/mvvm-xue-xi-vue-shi-jian-xiao-jie/)
刚刚看完上面这些，觉得自己too young too native
***
(继续愉快脸) 来谈谈你对spa的看法吧

(spa是个啥？？) 不好意思我没听清楚🙈
(正经脸) Single Page Application
(恍然大悟脸，不知道明显不明显) 我认为单页应用适合逻辑明确，需要组件复用的web应用。
我就一下讲我的项目举个栗子🌰吧~
例如项目中 header和footer的包括其中的一些 componet(about页面和登录页面)都是可以重复使用的。中间router-view部分的页面跳转通过vue-router来进行。
(好奇脸) 那spa如何优化？
(有点懵) 压缩css，js，减少http请求，在请求http时使用vue-resource ，在请求localStorage时使用对应的组件。
(愉悦脸) 你的意思是要清空缓存喽？
(🙈🙈其实并没有想到) 嗯嗯
***
(♪(^∇^*)) 那你为什么选择Vue呢？
(诚实的(。・・)ノ) 老师让。
(😓估计没想到我这么诚实) 那你自己的想法呢？
(思考脸) 比起Angular更加轻量，API更少，但是实用性蛮强。
(认真脸) 我觉得Vue也还是太重了,也就是说你在用它的时候没有考虑过为什么你们老师选择用Vue吗？
(此时我的脸色应该很苦/(ㄒoㄒ)/~~)
那我就说说我用的感受吧。
文档很详细，写法很简洁。
另外数据绑定没有Angular那么方便是双向，当model层一些复杂数据(例如数组)发生变化时，Vue是检测不到的，需要增加watch来监测这些变化。
没有RootScope，同级组件之间传递信息复杂。目前我的解决方法是，a先将信息冒泡到父组件父组件再广播b组件再接收。
(正经脸) ok，那其实框架只是一种选择。比起会用API更要紧的是你要知道为什么要选择它，了解它的优点和缺点，要知道框架中的功能都是怎么实现的
(疑惑脸) 那怎么去了解框架相关功能的实现？通过阅读源码吗？
(笑了) 有的框架源码可读性太差了况且如果对工程化没有一个很明确的理解的话读起来也是非常吃力的。
(小鸡啄米一样点头🐤)

(~\(≧▽≦)/~)我的问题结束了，那你有什么问题问我呢？
(这个部分我就不写，嘻嘻)

其实过了一天加上当时状态很糟糕，真正的过程应该远没有写的这么流畅，本来当时都准备背着包去上班了。
结果被叫住说我这关你过了，可以去外面等😳
![](http://7xspf8.com1.z0.glb.clouddn.com/1163471-ed34e4b6150f31b9.jpg)

二面明天再写