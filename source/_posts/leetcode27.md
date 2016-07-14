title: leetcode-27
date: 2016-02-15 22:05:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
```
Given an array and a value, remove all instances of that value in place and return the new length.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.
```
给定一个数组和一个值，删除该值的所有实例，并返回新的长度。
元素的顺序可以被改变，也不关心最终的数组长度

思路：先排个序
加了一个position数组来存储位置相关的信息
一开始没注意是返回number，以为返回nums
加了个length就好啦
```
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
 function removeElement(nums,val) {
        function compare(num1,num2){
            return num1 -num2;
        }
        nums.sort(compare);
        var position=[];
        for(var i=0;i<nums.length;i++){
            if(nums[i]==val){
                position.push(i);
            }
        }
        nums.splice(position[0],position.length);
        return nums.length;
    }
```
