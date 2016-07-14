title: Javascript忍者秘籍📒
date: 2016-06-24 11:02:36
categories: 归纳整理 #文章文类
tags: [JavaScript] #文章标签，多于一项时用这种格式
---

#### Chapter 3
##### 函数是第一型
1. 他们可以通过字面量进行创建
2. 他们可以赋值给变量，数组或其他对象的属性
3. 他们可以作为函数的返回值进行返回
4. 他们可以拥有动态的创建并赋值的属性
5. 此外函数还可以被调用( invoked )<一般以异步方式进行调用>

##### 浏览器的事件轮询
类似于图形用户界面( GUI )和桌面应用程序，事件轮询大多采用下面的机制：
1. 创建用户界面
2. 进入轮询，等待时间触发
3. 调用时间处理程序( addEventListener )

浏览器中，以下事件有可能穿插发生：
***浏览器事件，网络事件，用户事件，计时器事件***

浏览器的事件轮询是单线程的(single-threaded)。每个事件是按照队列中所放置的位置来处理的。

##### 回调
我们定义一个函数，以便其他的一些代码在合适的地方回头再调用它。
```
//使用比较器进行排序
//array.sort()方法有一个重载，接受一个包含比较方法的对象
var value = [ 1,34,23,65,12,9 ];
value.sort( function ( value1,value2 ){ return value2 - value1; });
```

##### 函数声明
1. 命名一个函数时，该名称在整个函数的声明范围内是有效的。如果一个函数声明在顶层，那么window对象上的同名属性将引用到该函数。

![函数会直接声明到顶层对象的同名属性](http://7xspf8.com2.z0.glb.clouddn.com/1163471-b33dedb26f6aff09.jpg)
1. 作用域
-   变量声明的作用域开始于声明的地方，结束于所在函数的结尾，与代码嵌套无关。
-   命名函数的作用域是指声明该函数的整个函数范围，与代码嵌套无关。
```
function outer(){
/* typeof inner ==='function' */ 
function inner(){
//some code here
}
}
```
- inner( )声明在整个 outer( )中都是可用的，而数字变量只是从声明处到函数结尾处才可被调用。函数在其作用域范围内可以被提前引用。

##### 函数调用

- 如果实际传入的参数数量大于函数声明的形参数量时，超出的参数不会配给形参名称。


- 当形参数量大于实际参数数量，则没有对应参数的形参会赋值为 undefined
- 所有的函数调用都会传递两个隐式参数：arguments和this
- arguments参数，类数组结构(可使用length，可使用下标)
- this参数，更适合称作调用上下文

1. 作为函数进行调用
```
function hello (){};
hello();
var hi = function(){};
hi();
```
以此种方法进行调用时，函数的上下文是全局上下文--window对象
1. 作为方法进行调用 --其上下文对象是方法的拥有者
2. 作为构造器进行调用 --其上下文对象是新创建的实例对象
3. apply()和call()可以显式的指定任何一个对象作为其函数上下文。 

#### Chapter 6 原型与面向对象
##### 1. 实例化和原型
- 对象实例化
JavaScript通过构造器执行 new 操作符来初始化一个新对象。
```
//声明一个对象，并将对象初始化到已知状态
var o = {};
o.name = 'Beginning';
o.age = 16;
o.job = 'front-end';
```
- 原型作为对象概览
函数作为构造器进行调用时，函数的原型是新对象的概览。
```
    function Ninja(){};
    Ninja.prototype.swingSword = function (){
      return true;
    }
    var ninja1 = Ninja();
    //此时对函数进行函数调用，则什么都没有发生
    // ninja1 = undefined 
    var ninja2 = new Ninja();
    //将函数作为构造器调用，不仅新对象实例被创建，而且函数原型上的方法也可以调用
  </script>
```
- 实例属性
使用 new 操作符将函数作为构造器进行调用时，其上下文被定义为新对象实例。除了通过原型给函数附加属性的形式之外，我们还可在构造器函数内通过this参数初始化值。
```
function Ninja(){
this.swung = false;
this.swingSword = function (){
return !this.swung;
}
}
Ninja.prototype.swingSword = function (){
return true;
}
var ninja2 = new Ninja();
//在构造器内创建的实例方法会阻挡在原型上创建的同名方法。
```
- 协调引用
***原型的改变会影响已经创建的对象***
***查找属性时，首先查找对象自身，如果没找到，再查找构造器原型***

##### 2.通过构造器判断对象类型
我们不用知道原有的构造器函数就可以再次创建一个新实例。
```
function Ninja(){};
var ninja = new Ninja(){};
var ninja2 = new ninja.constructor();
```
##### 3.继承与原型链
创建一个原型链最好的方法是，使用一个对象的实例作为另一个对象的原型。例如
```
//Ninja实例的原型将是Person的一个实例，该实例不仅拥有原型，还持有SuperClass的所有属性
Ninja.prototype = new Person();
```
![](http://img.keenwon.com/2016/03/20160314212504_39150.png)

```
function Super() {}
 
function Sub() {}
Sub.prototype = new Super();
Sub.prototype.constructor = Sub;
 
var sub = new Sub();
 
Sub.prototype.constructor === Sub; // ② true
sub.constructor === Sub; // ④ true
sub.__proto__ === Sub.prototype; // ⑤ true
Sub.prototype.__proto__ == Super.prototype; // ⑦ true
```
[http://keenwon.com/1524.html](http://keenwon.com/1524.html)
下面是一种可能的 forEach()实现
```
//先检查是否有原有方法
if(!Array.prototype.forEach){
Array.prototype.forEach = function (callback,context){
for ( var i = 0; i < this.length; i++ ){
//context||null 防止将undefined传递给call()
callback.call(context || null, this[i], i, this);
}
};
}
[a,b,c].forEach(function(value,index,array){
assert(value,"Is in position"+ index +"out of" +(array.length-1));
});
```
##### 编写类风格的代码
```
//通过Object创建一个Person类
var Person = Object.subClass({
init: function(isDancing){
this.dancing = isDancing;
},
dance: function(){
return this.dancing;
}
});
//通过Person创建一个Ninja类
var Ninja = Person.subClass({
init: function(){
this._super(false);
},
dance: function(){
return this._super();
},
swingSword: function(){
return true;
}
});

var person = new Person(true);
//person.dance() is true
var ninja = new Ninja();
//ninja.dance() is true
//ninja.swingSword() is true
//person instanceof Person is true
//Ninja is a Ninja and a Person
```