---
layout: post
title: "用openssl实现DES和AES算法时遇到的小问题"
date: 2017-04-13 22:52:16 +0800
comments: true
categories: 信息安全工程
keywords: file_not_found openssl链接库
tags: homebrew openssl mac
---
#### 问题1：可能因为是用homebrew安装的openssl，编译时找不到头文件，大概长这样：
```
'openssl/ssl.h' file not found
#include <openssl/ssl.h>
          ^
1 error generated.
```
解决方案：`xcode-select --install`
参考：[openssl/ssl.h not found but installed with homebrew](http://stackoverflow.com/questions/34178988/openssl-ssl-h-not-found-but-installed-with-homebrew)

<!--more-->

#### 问题2：遇到了`ld: symbol(s) not found for architecture x86_64`。
用g++也没用，在这卡了很久，搜到[Resolving symbol(s) not found for architecture x86_64](https://swift.unicorn.tv/articles/resolving-symbol-s-not-found-for-architecture-x86_64)，想了想应该是链接库的问题，搜到[关于openssl库的链接问题](http://blog.sina.com.cn/s/blog_45497dfa0100nxi3.html)，命令行编译时加上参数 -lssl -lcrypto就可以了。

-FIN-
