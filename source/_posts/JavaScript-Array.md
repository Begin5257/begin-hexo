title: JavaScript-Array
date: 2016-02-13 21:39:36
categories: 归纳整理 #文章文类
tags: [JavaScript] #文章标签，多于一项时用这种格式
---
1.定义
数组的标准定义是：一个存储元素的线性集合(collection)。
JavaScript的数组是一种特殊的对象，用来表示偏移量的索引是该对象的属性。
2.创建数组
-var numbers = [];  //这种方法效率更高,why?
-var numbers = new Array(10); //numbers.length 10
-var objects = [1,"Mary",true,null];
3.读写数组

```
//数据赋给数组
var numbers = [];
for ( var i=0; i<100 ;i++){
    nums[i]= i+1;
}
//读取数组
var numbers =[1,2,3,4,5,6,7];
var sum =0;
//使用length控制数组长度
for( var i=0 ;i<numbers.length; i++){
    sum +=numbers[i];
}
```

4.对数组进行整体性操作
当把一个数组赋给另一个数组时，只是为另一个数组增加了一个新的引用。当通过原引用修改数组的值时，另外一个引用也会感知到这个变化。
即新数组仍旧指向原来的数组。
```
var nums =[];
for( var i=0;i<100;i++ ){
    num[i]= i+1;
}
var samenums =nums;
nums[0]=400;
print(samenums[0]); // 400
```
一个更好的方案是采用深复制，将原数组的每一个元素都复制到新数组中。
```
funtion copy(arr1,arr2){
    for( var i=0;i<num1.length;i++){
        arr2[i]=arr1[i];
    }
}
var nums =[];
for( var i=0;i<100;i++ ){
    num[i]= i+1;
}
var samenums =[];
copy(nums,samenums);
nums[0]=400;
print(samenums[0]); // 400
```

5.由字符串生成数组
split()方法

6.存取函数
-查找元素 indexOf(),若目标数组包含该参数，则返回第一个参数的索引；若不存在，则返回-1;   var position = arr.indexOf(hello);
-lastIndexOf()返回最后一个参数的索引;
-join() 可以将数组转化为字符串 var str =arr.join();
-toString() 可以将数组转化为字符串  var str = arr.toString();
-concat() 合并数组  var newArr =arr2.concat(arr1);
-splice() 截取数组 var newArr =arr.splice(3,3) //第一个参数是起始索引，第二个参数是截取的长度

7.可变函数
-push() 为数组末尾添加元素 arr.push(6);
-unshift() 为数组开头添加元素 nums.unshift(1,2);
-pop() 可以删除数组末尾的元素 nums.pop();
-shift() 可以删除数组开头的元素 nums.shift();
这个是不使用方法的增加数组的第一个元素
```
var nums =[2,3,4,5];
var newnum =1;
for ( var =nums.length ; i>0; i++){
    nums[i]=nums[i-1];
}
nums[0] =newnum;
print(nums)//1,2,3,4,5
```
将删除的数组末尾元素追加的数组开始
```
var nums =[6,1,2,3,4,5];
var last=nums.shift();
nums.push(last);
print(nums);//1,2,3,4,5,6
```

8.从数组的中间位置添加或删除元素
采用splice()方法插入或删除元素，需要提供以下三个参数
-起始索引(希望开始添加元素的地方)
-需要删除的元素个数，添加元素时此项为0
-想要添加进数组的元素
```
//添加元素
nums.splice(3,0,[4,5,6]);
nums.splice(3,0,4,5,6);
//删除元素
nums.splice(3,4);
```

9.为数组排序
-reverser() 该方法将数组中元素的顺序进行翻转
-sort() 该方法对字符串数组按照字典顺序进行排序
```
function compare(num1,num2){
    return num1 -num2;
}
var nums =[3,2,5,6,4];
nums.sort(compare);
print(nums); //2,3,4,5,6
```

10.迭代器方法
    -forEach() 接受一个函数作为参数，对数组中每个元素使用该函数
    arr.forEach(square);
    -every() 接受一个返回值为Boolean类型的函数，对数组中每个元素使用该函数，若都为true，则返回true
    -some() 同上，但只要有一个为true，就返回true
    -reduce() 接受一个函数，返回一个值 对数组中所有元素进行累加
    -reduceRight() 同上，不过执行顺序从右到左
    -map() 生成新数组 类似forEach
    -filter() 同every，不过返回的是Boolean类型为true的元素
    
```
//reduce
function add (num1,num2){
    return num1+num2;
}
var nums = [1,2,3,4,5,6,7,8,9,10];
var sum =nums.reduce(add);
print(sum); //55

//map()
function curve(num){
    return num+=5;
}
var grades =[1,2,3,4,5];
var  new = grades.map(curve);
print(new); //6,7,8,9,10

//filter()
//过滤不包含cie的元素
function expectCie(str){
    if(str.indexOf("cie")>-1){
        return true;
    }
    return false;
}
var word = words.filter(expectCie);
```

