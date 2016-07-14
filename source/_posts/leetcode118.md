title: leetcode-118
date: 2016-02-15 22:06:36
categories: leetcode #文章文类
tags: [leetcode] #文章标签，多于一项时用这种格式
---
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

```
 function generate(numRows) {
        var number = new Array(numRows);
        for(var k=0;k<numRows;k++){
            number[k]=new Array(k+1);
            number[k][0]=1;
            number[k][k]=1;
        }
        for(var m=2;m<numRows;m++){
            for(var n=1;n<m;n++){
                number[m][n]=number[m-1][n-1] +number[m-1][n];
            }
        }
        return number;
    }
```
