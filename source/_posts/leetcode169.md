title: leetcode-169
date: 2016-02-15 22:01:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given an array of size n, find the majority element. The majority element is the element that appears more than ? n/2 ? times.

You may assume that the array is non-empty and the majority element always exist in the array.

先排个序。
然后突然发现，number出现的次数大于n/2
那就好办了，n/2之后的数不都是number嘛: )
```
/**
 * @param {number[]} nums
 * @return {number}
 */
 function majorityElement(nums) {
        function compare(num1,num2){
            return num1 -num2;
        }
        nums.sort(compare);
        var leng = nums.length;
        number =nums[Math.floor(leng/2)];
        return number;
    }
``` 
