title: 点滴云开发
date: 2016-04-07 12:02:36
categories: 开发总结 #文章文类
tags: [Vue.js] #文章标签，多于一项时用这种格式
---
线上地址：http://123.56.195.73/
1.webpack.base.config中，

```

output: {

path:path.resolve(__dirname,'../dist/static'),  //会build时在css和js之前加dist/static路径

publicPath:'/static/',  //build时会自动在图片文件之前加static路径

filename:'[name].js'

}

```

2.vue内的js需要

```

<script type='text/ecmascript-6'></script>

export default{

}

```

3.页面跳转会固定跳转到之前页面的位置，要加下面一行代码才行

```

router.beforeEach(function() {

window.scrollTo(0,0)

})

```

4.最新版本的vue在app.vue中必须return一个参数，否则build出的静态页面会报错。


5.如何使元素静止时是1px 的border，当鼠标hover时是3px的border而不引起元素浮动？

答 ：在平时设置3px颜色为transparent的border。如果要变圆角，则加overflow:hidden


6.stylus media query

答：

```

@mediascreenand(max-width:320px)

#content //注意层级关系

ul

width 85%

```

7.ios和OX渲染input时会默认在内部加上padding，导致同等height的button和input看起来并不相等;input会默认加border-radius


8.跑mongodb时会出现的错误：

Unable to create/open lock file: /data/mongod.lock errno:13 Permission denied

使用

$ sudo mkdir -p /data/db/

$ sudo chown `USERNAME` /data/db

通过 whoami 获取USERNAME

指定dbpath 启动 ./mongod  --dbpath /data/dbv

首页效果：![](http://7xspf8.com2.z0.glb.qiniucdn.com/homeweb.png)
移动端效果：![](http://7xspf8.com2.z0.glb.qiniucdn.com/homeh5.png)
