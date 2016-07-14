title: leetcode-26
date: 2016-02-11 23:05:00
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.


```
  function duplicates(nums) {
        if(nums.length<=1){
            return nums.length;
        }else{
            var leng =1;
            for(var i=1;i<nums.length;i++){
                if(nums[i] != nums[i-1]){ //不等于前一个元素，长度+1
                    nums[leng++] =nums[i]; //将新的元素装到前len个
                }
            }
            return leng;
        }
     }
```
