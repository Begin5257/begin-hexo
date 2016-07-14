title: resume-maker 1.0留念
date: 2016-04-19 21:01:36
categories: 开发总结 #文章文类
tags: [node] #文章标签，多于一项时用这种格式
---
在开始校招的时候，大家都在紧张的准备简历。
Sketch，PS，AI......
我？？ (⊙v⊙)那拿CSS做一个！

结果工作室蛮多小伙伴喜欢我的简历，于是就想说可不可以做一个简历生成器。
resume-maker 1.0就这样诞生啦~\(≧▽≦)/~
基本的思路是：
1. 实现登录，注册，登录保持
2. 保证表单填入的数据刷新不丢失
3. 主题颜色可更换
4. 使用 express + mongodb + jade + semantic-ui + stylus 实现

广受吐槽的简洁的不能再简洁登录界面：
![](http://7xspf8.com1.z0.glb.clouddn.com/1163471-4ebbc7ef5b1bda67.png)
广受吐槽的一口气填完必须否则强迫症会死表单界面：
![](http://7xspf8.com1.z0.glb.clouddn.com/1163471-22a87753bcebe4fc.png)

广受吐槽的为什么只有一个模板简历界面：
![](http://7xspf8.com1.z0.glb.clouddn.com/1163471-3d30f38fa8fac3a2.png)

麻麻我要设计%>_<%

其实过程还是蛮头疼的。
- 数据库的设计就是每位用户对应一份简历内容

- 采用 mongoose 与mongo连接。
因为简历需要的数据很多，所以每一个Schema里参数的定义就是一个大问题，我的解决方案是：给每一个参数定义一个类型( 有那么一点点心累 )

- 还有表单界面有些模块在添加完内容之后，需要让原先增加的模块继续保持存在。
我的解决办法是，将数据存入 localStorage，在生成页面时对 localStorage 中的数据进行判断，根据 localStorage 中的数据条数生成合适数量的表单并将 localStorage 中的数据展现在表单中。

- 主题颜色的控制：
目前全部采用 js 控制，but，即使原生js现在有了document.querySelectorAll这种类似作弊的 API ,还是很复杂啊(/≧-≦)/~┴┴ 
后来一拍脑门想起来我用的是 Stylus ......

- HTML语义化：
一定要起合适且美观的id及类名，不然 heheda(ps:今天在蜻蜓FM的控制台里面看到了heheda～)
主要是自己后期会疯：)

- cookie的控制( js发送cookie，node处理cookie )

因为被吐槽的地方太多，包括表单填写这种非常重要的交互方式。所以，我！要！重！构！
打算开始学习使用 react 框架，后端 Python ( 感谢后端小伙伴，再次鞠躬 )

线上链接：[http://resume-maker-e40c4.codingapp.com/](http://resume-maker-e40c4.codingapp.com/)
// 总之还是和我一起期待2.0吧 (⊙v⊙)
