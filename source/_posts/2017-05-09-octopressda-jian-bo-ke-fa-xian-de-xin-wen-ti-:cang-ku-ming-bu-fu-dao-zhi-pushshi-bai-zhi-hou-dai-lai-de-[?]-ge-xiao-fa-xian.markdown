---
layout: post
title: "octopress搭建博客发现的新问题「仓库名不符导致push失败」之后带来的一个小发现"
date: 2017-05-09 16:20:46 +0800
comments: true
categories: octopress
tags: octopress搭建博客
keywords: 博客搭建
---
## 发现问题
今天重新翻看这篇博客[mac电脑上搭建octopress博客](http://www.liuchungui.com/blog/2015/09/11/macdian-nao-shang-da-jian-octopressbo-ke/)的时候，发现了rake deploy命令是 **不会把博客的markdown文件提交到github的**，也就是说写完的博客markdown文件是只保存在本地的，一旦本地文件丢了，那就比较难复原了，虽然是「难」并不是「不能」，但本着多一事不如少一事少给自己找麻烦，还是把md文件提交上去比较好，就commit一下push一下的事情而已。

<!--more-->

于是我就参考这篇博客的写法，写了如下命令：
```
git add .
git commit -m '更新了饥荒新手向攻略、tex初体验并挖坑信安实验总结'
git push origin source
```
前两句都没问题，第三句报了错：
```
ERROR: Repository not found.
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

wtf?!我真的好方啊。我之前从来没深入了解过git以及octopress的原理，都是能用就行，其实一点都不懂。所以没办法，开始查呗。

## 解决问题
查到这篇[基于 Octopress & Github Pages 搭建博客（二）](http://www.jianshu.com/p/4d4a8cbe3f3e)，尝试了这个命令：`git remote -v`发现卧槽为啥我的仓库名不对啊？

这就不得不提到搭建博客的时候犯的错，教程说了要用username.github.io，我没用username，然后后来又改用的username，这个显示的仓库名是一开始没用username的那个现在已经不存在了的仓库……继续查，发现似乎没人犯过这么智障的错误……查不到什么。

于是我改搜错误提示：`Please make sure you have the correct access rights
and the repository exists.`查到[Git error: “Please make sure you have the correct access rights and the repository exists”](http://stackoverflow.com/questions/25927914/git-error-please-make-sure-you-have-the-correct-access-rights-and-the-reposito)，尝试了第一个答案，重置了一下url，然后就push成功了。

## 新的问题
本来觉得这应该就解决了吧，登上github看了眼自己的这个仓库，发现了：
```
Your recently pushed branches:
source
```
问我要不要「compare&pull request」。wtf?!

我当时已经方到智障了，根本没发现我之前就一个master分支，而自己刚刚push的是source分支……

## 小发现

继续查呗：[使用 Octopress+GitHub Pages 搭建个人博客](http://blog.leichunfeng.com/blog/2014/11/11/use-octopress-plus-github-pages-to-setup-a-personal-blog/)发现这一段：「**在这里，我还是想大概谈一谈 Octopress 的工作原理，不然你可能也会跟我刚接触 Octopress 时一样充满疑惑。Octopress 其实为我们建立了两个分支，一个是 source 分支，就像我们的书桌，用于存放我们书写时需要用到的各种工具，包括原始的 markdown 文件、生成博文用的插件、主题和脚本等等。另一个是 master 分支，其实就是 public 目录中的内容，用于存放最终生成的 HTML 博文。当我们执行 rake generate 命令时，Octopress 会为我们生成 HTML 博文到 public 目录下。当执行 rake deploy 命令时，Octopress 则会将 public 目录中的内容提交并同步到 GitHub Pages 。建议你自己亲自对比一下运行以上命令前后 octopress 目录中文件的变化，这样可以快速地熟悉 Octopress 的工作原理。**」

原来是这样子QAQ

## 参考：
1. [mac电脑上搭建octopress博客](http://www.liuchungui.com/blog/2015/09/11/macdian-nao-shang-da-jian-octopressbo-ke/)

2. [基于 Octopress & Github Pages 搭建博客（二）](http://www.jianshu.com/p/4d4a8cbe3f3e)

3. [Git error: “Please make sure you have the correct access rights and the repository exists”](http://stackoverflow.com/questions/25927914/git-error-please-make-sure-you-have-the-correct-access-rights-and-the-reposito)

4. [使用 Octopress+GitHub Pages 搭建个人博客](http://blog.leichunfeng.com/blog/2014/11/11/use-octopress-plus-github-pages-to-setup-a-personal-blog/)

5. [Octopress Blog由多台设备维护](http://changety.github.io/blog/2014/10/15/one-octopress-blog-on-mutil-place/)

6. [利用Octopress搭建一个Github博客](http://limite.me/blog/2013/09/17/da-jian-bo-ke-cao-zuo/)

-FIN-
