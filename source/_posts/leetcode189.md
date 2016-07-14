title: leetcode-189
date: 2016-02-11 19:31:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.


```
 function rotate(nums, k) {
   var long =nums.length;
   if(long==k){
     document.write(nums);
   }else{
       var delenums=nums.splice(long-k,long);
       for(var i=k-1; i>0 ;i--){
       nums.unshift(delenums[i]);
       }
      document.write(nums);
    }
}
```
报错报的我对人生都失去希望了，该换一种思路。
其实没有必要移动k次，移动k%n次就可以，因为中间的一些步骤都是重复循环
```
function rotate(nums, k) {
    var long =nums.length;
     k = k%long;
     dele = nums.splice(-k, k);
    after = nums.splice(-k, k); 
    nums = after.concat(nums); 
};
```
诶诶诶辣鸡你怎么还特么的报错！
呜呜原来没认真看注释的内容sad :（
```
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
```
哦辣鸡你居然不允许我给nums赋值，没关系我还有其他办法哈哈哈哈
```
function rotate(nums, k) {
  var long =nums.length;
  k = k%long;
  dele = nums.splice(-k, k);
  for(var i=k-1; i>=0 ;i--){
    nums.unshift(dele[i]); 
   }
}
```
哈哈哈哈终于过了可是还有两种方法，下次来填~

数组的一些方法：
-push() 为数组末尾添加元素 arr.push(6);
-unshift() 为数组开头添加元素 nums.unshift(1,2);
-pop() 可以删除数组末尾的元素 nums.pop();
-shift() 可以删除数组开头的元素 nums.shift();
采用splice()方法插入或删除元素，需要提供以下三个参数
-起始索引(希望开始添加元素的地方)
-需要删除的元素个数，添加元素时此项为0
-想要添加进数组的元素
