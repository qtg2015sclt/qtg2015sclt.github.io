---
layout: post
title: "用hexo搭建博客时遇到的一些问题"
date: 2017-04-15 00:02:05 +0800
comments: true
categories: hexo
keywords: hexo搭建博客
tags: 博客搭建
---
*最近写的笔记和文章开始多了，散落在各个文件夹里不好管理，想着自己搞个博客吧。去年这个时候师兄就跟我说可以搞起来了，结果又拖到现在……>_<*

就按照hexo官网文档一步步来吧:[Documentation](https://hexo.io/docs/#Requirements)

黑喂狗。
<!--more-->

## 安装node.js和git
都是用homebrew安装的，基本都是一个命令就安装了，非常方便。有的关于环境变量的什么什么还是没搞懂，等学了再说吧。（不知道直接到官网上下载一个会更方便吗？）

git自带了，不过之前都是新安装一个，git我也又装了一下，不知道会不会有什么影响。

**问题1：安装完npm没法用，大概这样：**
```
$ npm -v
-bash: npm: command not found
```
查了一下，有说用brew卸载了node重新在官网上下载安装，我觉得麻烦，就借助了一个回答，这样的：
```
$ brew postinstall node
```
（不用sudo，sudo好像brew会报错）
就OK了：
```
$ npm -v
4.2.0
```
参考：[NPM Command Not Found After Installing Node](http://stackoverflow.com/questions/32749549/npm-command-not-found-after-installing-node/32750036)的第三个回答，不过不需要用sudo。
之前也有遇到没有写权限不能安装时，我是笨笨地这样解决的：先sudo给/usr/local/bin开写权限`sudo chmod 777 /usr/local/bin`，然后安装完了再把写权限收回`sudo chmod 755 /usr/local/bin`。

## 安装hexo
`npm install -g hexo-cli`之后报错一大堆，也看不懂，看到permission denied，猜测可能又是权限问题？最后看到`Please try running this command again as root/Administrator.`……开了管理员权限，搞定。
(顺便用homebrew装了个tree）


## 结束
……（省略n步）

……基本上搞定了才发现……我觉得好看的那个博客，是用octopress搭建的……鉴于沉没成本不算成本，果断改去用octopress了。（虽然改个主题就好了，然鹅，找了好多hexo的主题都没有中意的……这都是借口，不管，就是想换，任性-。-）

这个应该不会再更新了……（我果然很坑……）

-FIN-
