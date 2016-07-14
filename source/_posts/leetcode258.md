title: leetcode-258
date: 2016-02-12 22:24:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.
这是根据定义写的
```
  function addDigits (num){
        var number = num;
        while(number>9){
            var  i =0;
            while(number){
                i+=(number%10);
                number=Math.floor(number/10);
            }
            number=i;
        }
        return number;
    }
};
```
一个数的数字根(digit root)就是将该数的所有数字加起来，循环往复，
直到只有一位数字为止。譬如 345， 3+4+5=12，1+2=3，
那么 345 的数字根就是 3。

leetcode 258: Add Digits 就是要计算非负整数的数字根。
 而root(10x+y) = root(x+y) 实际上 root(x) = x % 9 ；
 不过因为数 n 除了 0 时数字根是 0 之外，其他时候是取值 1 - 9，所以 n % 9 如果为 0 的时候数字根是 9 ！
 用一个小技巧处理便是： (n-1) % 9 + 1 ！
```
 function addDigits (num){
        return (num-1)%9+1;
    }
```
天惹居然只要一行代码就解决了！
