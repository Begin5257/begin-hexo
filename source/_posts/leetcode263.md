title: leetcode-263
date: 2016-02-19 20:02:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.


2,3,5

```
    /**
     * @param {number} num
     * @return {boolean}
     */
function isUgly(num) {
        if(num == 0) {
            return false;
        }
        while(num % 5 == 0) {
            num /= 5;
        }
        while(num % 3 == 0) {
            num /= 3;
        }
        while(num % 2 == 0) {
            num /= 2;
        }
        if(num == 1) {
            return true;
        }
        return false;
    }
```
