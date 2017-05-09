---
layout: post
title: "LeetCode2.Add Two Numbers题解报告"
date: 2017-04-20 23:24:11 +0800
comments: true
categories: LeetCode
tags: LeetCode题解报告
keywords: LeetCode 7.Reverse Integer
---
## 想法
注意进位。

<!--more-->

## 参考代码
*本来写的超级繁琐，因为while判断的是&&，其实判断||就可以了，以下代码是参考了论坛上的优质代码，改出来的第二版*
```c++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
      ListNode *p1 = l1, *p2 = l2;
      ListNode *result = new ListNode(0);
      ListNode *p = result;
      int c = 0;
      while(NULL != p1 || NULL != p2) {
        if(p1 != NULL) {
          c += p1->val;
          p1 = p1->next;
        }
        if(p2 != NULL) {
          c += p2->val;
          p2 = p2->next;
        }
        p->next = new ListNode(c % 10);
        p = p->next;
        c /= 10;
      }
      if(c != 0) {
        p->next = new ListNode(c);
      }
      return result->next;
    }
};
```

-FIN-
