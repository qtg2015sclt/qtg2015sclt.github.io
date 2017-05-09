---
layout: post
title: "Mac os X上openssl从安装到更新"
date: 2017-04-06 20:29:42 +0800
comments: true
categories: 从安装到卸载 信息安全工程
tags: 安装openssl
keywords: macOS安装openssl
---
##### *标题党了，其实就是从来没用过openssl的新手学着用的历程记录。*

信息安全课要做实验，要用openssl。
## step 1：
1. 打开官网：https://www.openssl.org/source/
要下载源码自己编译？还没搞过，想搜一搜怎么弄。
2. 然后顺手打开了终端，输入了`openssl version`
居然得到了回应`OpenSSL 0.9.8zh 14 Jan 2016`
说明已经有openssl了，应该不需要装了吧……
刚好看到一个博客：[Mac10.11升级安装openssl](http://www.liuchungui.com/blog/2016/05/10/mac10-dot-11sheng-ji-an-zhuang-openssl/)就一步步照做吧。

<!--more-->

##### *话说人家这个博客好漂亮啊，之前看华为的软挑一个大神分享，博客似乎也是长这样的，是自己搭的吗，好想自己也弄一个这么漂亮的博客。啊对了虽然软挑没上榜，但还是写个复盘吧，在这给自己挖个坑。好不跑题了，回来。*

## step 2：
3. 按博客上写的继续，所以`homebrew`是啥……
搜到`homebrew`的官网：https://brew.sh/index_zh-cn.html定位是：macOS 缺失的软件包管理器（The missing package manager for macOS）。wow
4. 把那句命令贴到自己的终端上，问你continue还是abort，当然continue了。然后稍等就安装好了。
5. `brew --version`查了下版本，是1.1.12，虽然是刚安装好的，但我的手不由自主地键入了`brew update`，没有报err，但是出了个warning：`Insecure world writable dir /usr/local/bin in PATH`然后就不动了，google了一下，得到：[How to solve Insecure world writable dir /usr in PATH,mode 040777 warning on Ruby?](http://stackoverflow.com/questions/26711249/how-to-solve-insecure-world-writable-dir-usr-in-path-mode-040777-warning-on-rub)搞定，warning不见了，但还是不动……

## step 3：
6. 不管了，继续`brew install openssl`（话说为啥是install？），结果brew竟然自己进入了更新`Updating Homebrew`，然后就不动了，令人绝望。不过毕竟说了更新会比较久，那就耐心等吧。
7. 其实并不久，一会就好了，开始下openssl，结果竟然超时没下下来，但是没结束，开始安装openssl的依赖，然后换了个地址继续下openssl……省略中间过程若干（自己注意一点看看警告和错误然后照做就好比如要自己手动`brew link makedepend`，因为文件夹权限问题没写进去）
8. 现在好像大概明白为啥是install了，使用openssl是用新安装的，似乎虽然自带openssl的样子但好像不用自带的（想起了python……虽然上次就是用了自带的）

## step 4:

9. 卡在最后一步了……用不了第二种方法 ，现在去重启搞第一种，回来继续……
10. `OpenSSL 1.0.2k  26 Jan 2017`成功~

-FIN-
