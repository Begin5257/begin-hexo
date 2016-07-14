title: leetcode-58
date: 2016-02-16 21:00:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---

Given a string s consists of upper/lower-case alphabets and 
empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

For example, 
Given s = "Hello World",
return 5.

```
/**
 * @param {string} s
 * @return {number}
 */
 function lengthOfLastWord(s) {
    var sArray = s.split(" ");
    //撸掉那些长度等于0的元素
    sArray = sArray.filter(function(str){
            return str.length > 0;
    })

    if(sArray.length > 0) {
        var lastWord = sArray[sArray.length - 1];
        return lastWord.length;
    } else {
        return 0;
    }
    }
```
