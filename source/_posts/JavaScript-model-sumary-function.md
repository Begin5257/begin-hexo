title: JavaScript设计模式读书笔记----字面量和构造函数,函数
date: 2016-04-16 21:01:36
categories: 归纳整理 #文章文类
tags: [设计模式] #文章标签，多于一项时用这种格式
---
1. 当以 new 操作符调用构造函数时， 函数内部将会发生以下变化：
> 创建一个空对象并且 this 变量引用了该对象，同时还继承了该函数的原型；
   属性和方法被加入到 this 引用的对象中；
   新创建的对象由 this 引用，并且最后隐式的返回 this ；

 ```
var Person = function (name) {
  //使用对象字面量模式创建一个新对象
  var this = {} ;
  //向this添加属性和方法
  this.name = name;
  this.say = function () {
    return "I'm" + this.name;
  }  
//return this;
};
//一般情况下，将一个方法添加到Person的原型
Person.prototype.say = function () {
  return "I'm" + this.name;
}
```
2. 当使用new操作符创建对象时，构造函数总是返回一个对象。默认返回this所引用的对象，将返回空； 
3. 检测数组的方法 :
 ```
if ( typeof Array.isArray === "undefined" ) {
  Array.isArray = function (arg) {
  //调用Object.prototype.toString()的call()方法， 如果是数组返回[object Array]，对象返回[Object Object]
    retrun Object.prototype.toString.call(arg) === "[object Array]";
    };
}
```
4. 函数的提升
```
function foo () {
  alert("global foo");
}
function bar () {
  alert("global bar");
}
function hoistMe() 
  console.log(typeof foo); // "function"
  console.log(typeof bar); //"undefined"

  foo(); // "global foo"
  bar(); // TypeError: bar is not a function
  //函数声明，变量"foo"及其实现者被提升
  function foo ()  {
    alert("local foo");
  }
  //函数表达式，仅变量"bar"被提升，函数实现并未被提升
  var bar = function () {
    alert("local bar");
  };
}
hoistMe();
```
5. 异步事件监听器
  ```
document.addEventListener("click",function(){alert("hello~")},false);
```
6. 即时函数
即时函数模式(Immediate Function pattern)是一种可以支持在定义函数后立即执行该函数的语法。
 ```
(function () {
     alert("looooooook!");
}());
//在函数末尾添加一组括号，这导致该函数立刻执行
//将所有代码包装到它的局部作用域中，切不会将任何变量泄露到全局作用域之中
```
7. 即时函数的返回值
可以利用即时函数包装一个在对象生存期内不会改变的属性，并且即时函数的返回值会成为属性值。
 ```
var  o = {
  message: (function(){
     var who = "me",
         what = "call";
    return what+" "+who;
}()),
getMsg: function () {
  return this.message;
    }
};
o.getMsg(); //输出"call me"
o.message; //输出"call me"
```
8. 即时函数的初始化
 ```
({...}).init();
({...}.init());
//如果要在init()结束后保存对该对象的一个引用，可以通过在init()后面添加"return this"实现该功能;
```
9. 备忘模式
函数 myFunc 创建了一个属性cache，cache属性是一个对象(哈希对象)，使用传递给函数的param作为键，结果为值。
```
var myFunc = function () {
    if ( !myFunc.cache[param] ) {
      //一些操作
      var result = {};
      myFunc.cache[param] = result; 
     }
    return myFunc.cache[param];
}
```
10. 配置对象
```
//before
function addPerson (name,age,birth,address,gender,first,last){......}; 
addPerson("begin","16",'123","女","b","g");
//after
var conf = {
      name:"begin",
      first:"b",
      last::"g",
      gender:"女"
}；
addPerson(conf);
```
优点：不需要记住众多的参数及其顺序，可以安全忽略可选参数，易于阅读和维护，易于添加和删除参数。

11. call()和apply()的区别
[http://www.jianshu.com/p/3a823ef9db97](http://www.jianshu.com/p/3a823ef9db97)

12. Curry化 //需要深入了解
 当新函数是基于现有函数，并加上部分参数列表创建时。

总结：
1. API 模式：
  - 回调模式：将函数作为参数进行传递
  - 配置对象：便于控制函数的参数数量
  - 返回函数：当一个函数的返回值是另一个函数时
  - Curry化：当新函数是基于现有函数，并加上部分参数列表创建时
2. 初始化模式
  - 即时函数 ：定义后立即的函数
  - 即时对象初始化：匿名对象组织了初始化任务，提供了可以被立即调用的方法
  - 初始化时分支：帮助分支代码在初始化时仅检测一次
3. 性能模式
  - 备忘模式：使用函数属性以便计算过的值无需再次计算
  - 自定义模式：以新的主体重写本身，使得后续调用时进行的工作更少 
