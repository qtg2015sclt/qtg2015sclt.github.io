---
layout: post
title: "用octopress搭建博客时遇到的一些问题"
date: 2017-04-15 22:30:04 +0800
comments: true
categories: octopress
tags: octopress搭建博客
keywords: 博客搭建
---
换了octopress，其实感觉差不多……基本上遇到的问题都被人解决过了，只要搜索技能过关都能搞定。

主要参考了：[mac电脑上搭建octopress博客](http://www.liuchungui.com/blog/2015/09/11/macdian-nao-shang-da-jian-octopressbo-ke/)

### 写一下按照上述博客来做的过程中遇到的问题
问题1：`rake deploy`的时候遇到如下：
```
ERROR: Repository not found.
fatal: Could not read from remote repository.
```
<!--more-->
解决：（重新）`$ rake setup_github_pages`
要输入github的用户名和密码。

问题2：域名这一块搞了好久，其实按照github pages上的说明来就好（在仓库的setting的github pages那一栏，当自己的域名没有被正确解析时会有个说明的链接），再附一个参考吧：[git系列三 利用github pages快速搭建个人网站](http://www.jianshu.com/p/3a14ff2ff351)
（其实在dnspod上添加的时候还遇到了「记录的值不正确」（好像是，有点忘了）的问题， 夜里想破脑袋也没搞清楚，估计是困糊涂了，睡醒了发现该填CNAME的地方填成了A……QAQ）

*域名可以访问啦，开心ww*

问题3：在categories这里显示的是{百分号 category_list 百分号}而不是真正的分类列表。
解决：
参考：[为octopress添加分类(category)列表](http://codemacro.com/2012/07/18/add-category-list-to-octopress/)

问题4：遇到deploy失败的时候
```
$ rake deploy
...
Server aborted the SSL handshake...
...
```
搜了一下，我最终选择再deploy一遍

---
选了一个比较喜欢的主题，推荐：[Whitespace](https://github.com/lucaslew/whitespace)
预览就看我的新博客吧ww：[风怜目尽无疆地s Space](http://www.fenglians.com/)

目前就这些问题了，如果再遇到问题，以及还想调整一些细节，还会做记录，但不一定会在这更新了。

---
记录一下还想调整的地方，就根据这篇文章调整吧：[自定义你的Octopress博客](http://foggry.com/blog/2014/04/28/custom-your-octopress-blog/)

-TBC-
