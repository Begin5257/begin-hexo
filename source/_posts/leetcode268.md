title: leetcode-268
date: 2016-02-12 20:32:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2.

Note:Your algorithm should run in linear runtime complexity. 
Could you implement it using only constant extra space complexity?
```
function missingNumber (nums) {
        var leng = nums.length;
        var sum = (leng+1)*leng/2;
        var numsSum=0;
        for(var i=0;i<leng;i++){
            numsSum+=nums[i];
        }
        return sum-numsSum;
    }
```
