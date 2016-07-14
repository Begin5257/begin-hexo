title: leetcode-66
date: 2016-02-15 22:04:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given a non-negative number represented as an array of digits, plus one to the number.
The digits are stored such that the most significant digit is at the head of the list.

思路：
1.除最高位外，每一位若为9，+1后为0；
2.若不为9，就还是原来的数字；// sum = (push + digits[i]) % 10;
3.若最高位仍有进位，那便使进位值为1，加到number数组的第一位；
//push=Math.floor((push+digits[i])/10);

```
 function plusOne(digits) {
         var  number=[];
         var push=1;
         var n=digits.length-1;
         var sum=0;
         for(i=n; i>=0; i--) {
             sum = (push + digits[i]) % 10;
             //if(digit[i]==10){push=2}
             push=Math.floor((push+digits[i])/10);
             number[n]=sum;
             n--;
         }
         if(push!==0) {
             number.unshift(push);
         }
         console.log(number);
     }
``` 
