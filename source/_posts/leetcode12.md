title: leetcode-12
date: 2016-02-16 23:00:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---

Integer to Roman
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.
罗马数字简介：
https://zh.wikipedia.org/wiki/%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97

使用贪心算法，注意900,400,90,40,9,4
```
/**
     * @param {number} num
     * @return {string}
     */
function intToRoman(num) {
        var roman =[];
        var str =[ "M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I" ];
        var value =[1000,900,500,400, 100, 90,  50, 40,  10, 9, 5, 4, 1];
        for(var i=0; num!=0; ++i){
            while(num >= value[i]){
                num = num - value[i];
                roman.push(str[i]);
            }
        }
        return (roman.join(""));
    }
```
好多坑= =
1.最开始采取了枚举，一堆循环要上天
2.看了discuss，原来可以贪心呀
3.900,400,90,40,9,4算着太烦直接枚举就好了
4.最后用join转换成字符串，才发现如果在括号里填什么，就会用符号分开，如果不填，就默认逗号(之前真的没印象，逃~)


顺手翻到的一篇总结JavaScript字符串很好的文章
http://riny.net/2012/the-summary-of-javascript-string/
