title: leetcode-283
date: 2016-02-12 19:06:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function,
 nums should be [1, 3, 12, 0, 0].
 
```
 function moveZeroes(nums) {
         for(var i=0;i<nums.length;i++){
             var index =nums.indexOf(0);
             if(nums[index]==0){
                 nums.push(0);
                 nums.splice(index,1);
             }
          }
     }
```
