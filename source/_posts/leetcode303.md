title: leetcode-303 
date: 2016-02-10 23:32:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Range Sum Query
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example: Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
Note: You may assume that the array does not change. There are many calls to sumRange function.

宝宝最开始的解法，超时了: (
```
var NumArray = function(nums) {
   
};
NumArray.prototype.sumRange = function(i, j) {
    var sum=0;
        for(var k=i;k<j;k++){
            sum+=NumArray[k];
        }
        return sum;
};
```
换了一种解法，用Java
```
public class NumArray {
    int[] sums;
    public NumArray(int[] nums) {
        sums = new int[nums.length + 1];
        int sum = 0;
        sums[0] = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            sums[i + 1] = sum;
        }
    }
    
    public int sumRange(int i, int j) {
        return sums[j + 1] - sums[i];
    }
}
```
最后回到JavaScript，通过了~
```
function NumArray(nums) {
    this.nums = nums;
    var sums = [];
    this.sums = sums;
        this.sums.length = this.nums.length;
        this.sums[0] = this.nums[0];
        for (var i = 1; i < this.nums.length; i++) {
            this.sums[i] = this.sums[i - 1] + this.nums[i];
        }
}

NumArray.prototype.sumRange = function (i, j) {
    if (this.sums == null) {
        return 0;
    }
    if (i >= this.sums.length || j >= this.sums.length || i > j) {
        return 0;
    } else if (i == 0) {
        return this.sums[j];
    } else {
        return this.sums[j] -this.sums[i - 1];
    }
};
```
