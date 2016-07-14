title: leetcode-13
date: 2016-02-16 22:00:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Roman to Integer
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

感觉思路被上一道题困住了(快放开我！)
```
function romanToInt(s) {
        var int =[];
        var str =[ "M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I" ];
        var value =[1000,900,500,400, 100, 90,  50, 40,  10, 9, 5, 4, 1];
        for(var i=0; i< s.length; i++){
            for(var j=0;j<str.length;j++){
                if(s[i]==str[j]){
                    int.push(value[j]);
                }
            }
        }
        console.log(int);
        var intsum=0;
        for(var j=0;j<int.length;j++){
            intsum+=int[j];
        }
        console.log(intsum);
    }
```
然而我不太清楚怎么区分两个数组排在一起用js写的方法

```
public int romanToInt(String s) {
    HashMap<Character, Integer> values = new HashMap<Character, Integer>();
    values.put('I',1);
    values.put('V',5);
    values.put('X',10);
    values.put('L',50);
    values.put('C',100);
    values.put('D',500);
    values.put('M',1000);

    int ptr = s.length() - 1;
    int curr;
    int prev = 0;
    int result = 0;

    while(ptr >= 0) {
        curr = values.get(s.charAt(ptr));
        result = curr >= prev ? (result + curr) : (result - curr);
        prev = curr;
        ptr--;
    }

    return result;
}
```
熬，hashtable
明天再看
