---
layout: post
title: "LeetCode 7.Reverse Integer题解报告"
date: 2017-04-20 16:21:14 +0800
comments: true
categories: LeetCode
tags: LeetCode题解报告
keywords: LeetCode 7.Reverse Integer
---
## 想法
翻转一个int型的数并不难，主要是要判断溢出。既然溢出是由于int型的内存空间限制导致的，那声明一个long long的变量就可以避免int型的溢出，两个变量做同样的操作，最后比较两者是否相等，不相等就是溢出了。

<!--more-->

## 代码
```c++
class Solution {
public:
    int reverse(int x) {
      long long tmp = 0;
      int result = 0;
      int flagBelowZero = 0;
      if(x < 0) {
        flagBelowZero = 1;
        x = -x;
      }
      while(x)
      {
        result = result * 10 + x % 10;
        tmp = tmp * 10 + x % 10;
        x /= 10;
        //printf("result = %d, tmp = %lld\n", result, tmp);
      }
      if(1 == flagBelowZero) {
        result *= -1;
        tmp *= -1;
      }
      //printf("result = %d, tmp = %lld\n", result, tmp);
      if(result != tmp) {
        //printf("hello\n");
        result = 0;
      }
      return result;
    }
};
```

## 更好的想法
其实只要找到溢出的那个操作就好了，不需要全操作完了才判断。想法来自别人，就不把代码放这了，部分伪码如下：
```c++
while(x)
  tmp = result * 10 + x % 10;
  if(tmp / 10 != result)
    该步操作溢出
```

-FIN-
