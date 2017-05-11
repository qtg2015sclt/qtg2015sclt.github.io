---
layout: post
title: "工程实践kiwiCam的进展记录"
date: 2017-05-09 21:42:54 +0800
comments: true
categories: iOS
tags: iOS
keywords: iOS
---
> 工程实践进展不下去了，打算参照一个开源项目重新规划重新来过。持续更新吧，最近就搞这个了

## 2017.05.09

### 对开源项目Capture的分析
项目地址：[Capture](https://github.com/dulingkang/Capture)一个一个group来分析好了：

<!--more-->

0. 该项目是使用swift语言写的，我也打算用swift来写

1. 裁剪功能是使用的第三方提供的，语言是oc

2. Home中主要实现了主界面的view和controller

3. SeniorBeauty是选择好图片后的三个高级功能：模糊、贴图、滤镜；以及该界面相关的MVC（其实功能有四个，还有一个就是裁剪）

4. Camera是实现实时滤镜的，目前我不打算做这个功能，就直接调用自带的相机拍个照就可以了

5. Global，目前我的理解是定义了一些全局使用的view和model

6. Lib
    - OpenSource中应该是用来分享的接口
    - （百度广告就不提了）剩下一堆framework，不知道是什么，查一查之后再来更新

7. Util，应该是实用工具吧，但是不知道那四个文件用来干嘛的，一样，查完搞清楚之后回来更新

8. Resource里主要是用到的图片资源和info.plist。该项目基本没有使用storyboard，纯手工写view，我也打算这么写了

### 目前的计划
1. 这次就不作妖了，人家怎么写的就搞清楚之后自己写起来，不在大方向上随便瞎改了

2. 就从第一个commit开始看，一步步来写吧

-TBC-
