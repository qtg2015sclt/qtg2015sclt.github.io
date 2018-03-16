---
layout: post
title: "iOS 多线程相关...to be continued..."
date: 2018-03-16 20:31:16 +0800
comments: true
categories: iOS
tags: iOS 多线程
keywords: iOS 多线程
---
> 小声逼逼: 好久（一年）不写 blog 了, 为什么又写起来了呢, 因为今天接了个突然袭击的电话面试, 然后被问到懵逼... 其实问的并不难都能聊两句但是都不太懂, 是我自己太渣. 想想自己这实习的大半年, 都没啥长进, 好伤心QAQ. 面试官的建议是, 多思考多总结. 真的很感谢, 要不是这个面试, 不知道我还要飘到什么时候去... 我运气真好.
先来总结一点多线程相关的东西, 欢迎指正

## 进程与线程的区别

- 进程是资源分配的最小单元, 线程是程序执行的最小单元.

- 每个线程都运行在进程的上下文中, 共享同样的代码和全局数据. *所以线程天然地就具有能够更为方便的共享数据的优点啊, 但也容易引发线程安全上的问题*

<!--more-->

- 进程切换需要切换上下文, 而线程由于共享了进程的上下文, 切换线程并不会切换上下文.

- 进程有自己的地址空间, 而线程没有, 线程必须依赖进程而存在. 线程有自己的栈和栈指针.

- 待补充...

## iOS 中的多线程技术 简介
> 我只用过 GCD, 听说过 NSThread, 其他两个...

1. Pthreads
2. NSThread
3. GCD
4. NSOperation & NSOPerationQueue

### Pthreads
即 POSIX Threads, 一套通用线程库, 在类 Unix 操作系统中都使用它作为操! 作! 系! 统!的线程. *可以说非常厉害了呢, 但也就非常底层*
基于 C语言 的框架, 定义了一整套如何创建和操纵线程的 API. *swift 写多了看 C 会想吐吧. 我写 C 的时候到没有想吐, 但看到 OC 是很 feel sick 了*

*不多说 Pthreads 了, 真正 iOS 开发中应该基本不会用到, 列个参考在后面, 需要看的时候去看一下*

### NSThread

苹果把 POSIX Threads 封装了, 变成面向对象的, 一个线程一个对象, 就可以直接操控线程对象. 但依然很难用, 所有的线程活动都需要自己手动管理.

*所以用的时候就是很 OC 地先创建一个对象, 然后调用启动线程的方法.*



## 参考
1. [关于iOS多线程，你看我就够了](https://www.jianshu.com/p/0b0d9b1f1f19)
2. [POSIX Threads Programming](https://computing.llnl.gov/tutorials/pthreads/)
3. [POSIX 线程详解](https://www.ibm.com/developerworks/cn/linux/thread/posix_thread1/index.html)
4. [iOS多线程总结](https://segmentfault.com/a/1190000006612189)

-TBC-
