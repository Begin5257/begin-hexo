title: JavaScript 例子
date: 2016-02-09 16:29:21
categories: 归纳整理 #文章文类
tags: [JavaScript] #文章标签，多于一项时用这种格式
---
看书时候遇到这样一个例子，依次点击4个li标签，正确的运行结果是？
```
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>
<script>
  var elements = document.getElementsByTagName("li");
  for (var i=0;i<elements.length;i++){
     elements[i].onclick =function( ){
       alert(i); // 4 4 4 4
     };
  }
```
 
本来天真的以为，3 3 3 3 嘛，每个函数的作用域链中都保存着return 的活动对象，变量i的值都应该是3
but，答案是4 4 4 4 ，诶诶诶？
后来想了想，for循环可以等价于下面的while循环


while(i<4){
   console i;
    i++;
}


这货的循环停止后的i是4啊~

下面是依次点击4个li标签，正确显示1 2 3 4的写法
创建一个匿名函数强制闭包~
```
var elements = document.getElementsByTagName("li");
  for (var i=0;i<elements.length;i++){
    elements[i].onclick =function(num){
      return function(){
        alert(num);
      };
    }(i);
  }
```
