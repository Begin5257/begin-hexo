title: leetcode-326
date: 2016-02-10 23:31:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Power of Three
Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?
```
var NumArray = function(nums) {
    nums = [-2, 0, 3, -5, 2, -1];
};

NumArray.prototype.sumRange = function(i, j) {
    //var nums = [-2, 0, 3, -5, 2, -1];
    var sum=0;
        for(var k=i;k<j;k++){
            sum+=NumArray[k];
        }
        return sum;
};
```
