title: JavaScript设计模式读书笔记----基本技巧
date: 2016-04-14 21:01:36
categories: 归纳整理 #文章文类
tags: [设计模式] #文章标签，多于一项时用这种格式
---
1. 编写可维护的代码
2. 尽量减少全局变量
> 没有声明或没有对链式赋值的所有变量进行声明时也生成全局变量
  隐含全局变量可以通过delete删除，明确定义的全局变量则不可以。隐含全局变量是全局对象的属性。
3. 不要增加内置对象的原型。
4. 优化 for 循环

 ```
//一般情况
for( var i = 0;i < arr.length ; i++ ) {
  //处理 arr[i]
}
//但是每次访问任何容器的长度时，都是在查询活动的 DOM ，应该减少这种 DOM 操作
//优化之后
var length = arr.length ; 
for( var i = 0;i < length ; i++ ) {
  //处理 arr[i]
}
//最优
var i,arr = [];
for ( i = arr.length ; i-- ) { //使用最少的变量；逐步减至0，因为与0比较比与数组长度比较更有效率
  //处理 arr[i] 
}
//或使用 while 循环
var arr = [];
      i = arr.length;
while ( i-- ) {
  //处理 arr[i] 
}
```
5. for-in
 ```
for ( var i in man ) {
  if ( man.hasOwnProperty(i)) {
    console.log(i);
    }
}
```
5. 不要使用setInterval( ),setTimeout( )等构造函数来传递参数。
6. 不要使用 eval( ), 可以使用 new Function ( ) 来替代或将 eval( ) 封装在一个即时函数中
  //eval( )会影响到作用域链，可以访问和修改它外部作用域的变量
7. 字符串转化为数字的方法：

 ```
parseInt("08",10) //注意一定要给第二个参数赋值
+"08" // 8
Number("08"); //8
```
8. 命名约定
> 构造函数的首字母大写
   变量名和函数名采用驼峰命名法
   大写的变量名约定该变量在程序生命周期中不可改变
   JSLint 会对下划线前缀给出警告
