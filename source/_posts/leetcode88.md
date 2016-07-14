title: leetcode-88
date: 2016-02-15 22:02:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
 The number of elements initialized in nums1 and nums2 are m and n respectively.
 
 给定两个排序的整型数组nums1和nums2，将nums2合并到nums1成一个排序数组。
 
Note：
 你可以假设nums1中有足够的空间（空间大于或等于m+n）来存放来自nums2的额外元素。
 nums1和nums2的初始空间分别是m和n。
 
 思路：
 1.nums1的空间不足时，num1末尾的元素要舍掉；
 //注意先给nums1.length赋值；不要直接在while的判断条件里使用nums.length
 2.nums2空间不足时，循环会判断添加的元素个数；
 3.最后排个序就好啦~
```
 function merge(nums1, m, nums2, n) {
         var k=m;
         var len=nums1.length;
         while(k<len){
                 nums1.pop();
                 k++;
         }
         for(var i=0;i<n;i++){
             nums1.push(nums2[i]);
         }
         function compare(num1,num2){
             return num1 -num2;
         }
         nums1.sort(compare);
     }
```
