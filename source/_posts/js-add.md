title: JS求和方法总结
date: 2016-05-24 12:02:36
categories: 归纳整理 #文章文类
tags: [JavaScript] #文章标签，多于一项时用这种格式
---
```
//normal
var array = [1,2,3];

var sum1 = 0;
for(var i = 0 ;i < array.length ;i++) {
sum1 += array[i];
}
console.log(sum1);

// array.reduce
var sum2 = array.reduce(function (a,b) {
return a+b;
});
console.log(sum2);

// array.map
var sum3 = 0;
function getSum(item, index, array) {
sum3 += item;
}
array.map(getSum);
console.log(sum3);

// _.reduce
var sum4 = _.reduce(array, function(a, b){
return a + b;
});
console.log(sum4);

// _.reduceRight
var sum5 = _.reduceRight(array,function (a,b) {
return a+b;
});
console.log(sum5);

//邪恶的eval
var sum6 = eval(array.join("+"));
console.log(sum6);

//for in
var sum7 = 0;
for( var i in array ) {                                             
    sum7 += array[i]                     
}
console.log(sum7);
```
