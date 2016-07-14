title: leetcode-228
date: 2016-02-10 20:41:26
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---

Given a sorted integer array without duplicates, return the summary of its ranges.

For example, given [0,1,2,4,5,7], return ["0->2","4->5","7"].


```
/**
 * @param {number[]} nums
 * @return {string[]}
 */
function summaryRanges(nums) {
         var result =[];
         var leng =nums.length;
         if(leng==0){
             return result;
         }
         if(leng==1){
             return [nums.toString()];
         }
         for(var i=0;i<leng;)
         {
             var start=i;
             var end=i;
             //当后面一个元素等于前面一个元素
             while ((end + 1 < leng) && (nums[end] == nums[end + 1] - 1)){
                 end++;
             }
                 if (start < end) {
                     var str = nums[start].toString() + "->" + nums[end].toString();
                     result.push(str);
                     i = end + 1;
                 } else {
                     var stt = nums[start].toString();
                     result.push(stt);
                     i = end + 1;
                 }
             }
             return result;
     }
```


