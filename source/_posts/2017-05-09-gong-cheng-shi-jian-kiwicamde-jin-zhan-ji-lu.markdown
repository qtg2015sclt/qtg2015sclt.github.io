---
layout: post
title: "工程实践kiwiCam的进展记录...to be continued"
date: 2017-05-17 21:42:54 +0800
comments: true
categories: iOS
tags: iOS
keywords: iOS
---
> 工程实践进展不下去了，打算参照一个开源项目重新规划重新来过。  
持续更新吧，最近就搞这个了。
加粗是待填的坑。   
警告：大部分内容都是个人猜测，是记录给自己看的，除此以外不具备任何参考性。

*最近开了门课天天要上课写作业，没时间写工程实践；而且鉴于之前效率不够高，我要换个方案了……*

<!--more-->

* TOC
{:toc}

# 2017.05.15-present
*一个题外：我只是想给文章插个目录而已，atom上装package生成的toc是不能在网站上显示出来的（事实上我都没能调出来，难道markdown和md后缀不同么……），不废话了，参考这篇：[Jekyll kramdown配置 ](http://blog.javachen.com/2015/06/30/jekyll-kramdown-config.html)*
## home group
### Controller
按照Capture稍微修改了一下`HomeViewController`，对有疑问的地方想模拟一下来比较试试。（用真机模拟的时候……居然手机上的系统版本太高要更新xcode。）
```swift
self.navigationController?.setNavigationBarHidden(true, animated: false)
```
1. 之前不是给`HomeViewController`添加了个`NavigationControllerScene`吗，所以猜测这句话是隐藏导航Bar的，于是试了一下，果然写上这句上面那个导航Bar就不见了。那为什么还要添加Navigation呢？**一个猜测：大约是后面有些功能需要（比如修图的时候用到的「返回」啊「下一步」啊什么的）。**  

2. 加上「?」是指是可选类型，也就是说可能有`NavigationController`，也可能没有（为nil）。猜测：如果有的话就使用「.」之后的这个方法，如果为空就不调用这个方法。

### View
1. 创建文件`MainScrollView.swift`，并不是现有的`HomeView.swift`，应该是后来改名了。翻了一下commit，本来创建的是一个`UIScrolView`，后来删掉改成了`UIView`，所以我就直接写后者吧。（**关于滚动视图和View的区别，还有待继续了解。**）

2. 新建的`HomeView`继承了UIView，但后面还有一个`UIScrollViewDelegate`，**是多继承吗？以及这个Delegate又是起到了哪些作用？**  
因为之前只了解了swift的一点点基础语法，趁此机会去了解一下类相关的，参考[类和结构体](http://wiki.jikexueyuan.com/project/swift/chapter2/09_Classes_and_Structures.html)。
> 提到了命名方式，`UpperCamelCase`和`lowerCamelCase`，我以前还没有注意过，以后写代码的时候注意。  
类实例没有结构体的默认成员逐一构造器。  
结构体和枚举是值类型（基本类型都是值类型）：被赋予或传递时，会拷贝值。  
而类是引用类型。关于声明一个常量引用却可以更改其属性，我的理解是就想cpp里的常指针`int * const p = a`，不能改的是其指向，而指向的内容可变。

3. `override init`是由于HomeView类是UIView的子类，需要重写父类的init函数，……其他参考[从 Swift 初始化说起 ](http://huizhao.win/2016/11/13/swift-init/)。还有版本变化的问题，也要相应地进行改写。  

4. 声明为`CGFloat!`，~~为什么不是Float？~~ 参考[What's the difference between using CGFloat and float?](http://stackoverflow.com/questions/1264924/whats-the-difference-between-using-cgfloat-and-float) **为什么要加「!」**，尝试了一下把「!」去掉，在初始化器中就会报错（好像是因为需要在初始化器中进行初始化）。  

5. 获取屏幕尺寸，参考[Swift: Determine iOS Screen size [duplicate]](http://stackoverflow.com/questions/24110762/swift-determine-ios-screen-size)。

6. 不写修饰符的时候默认是let

7. UIPageControl参考官方网页：[UIPageControl](https://developer.apple.com/reference/uikit/uipagecontrol)

8. view的init

## LaunchScreen.storyboard和Main.storyboard
给view上加了个图片。为了适合各种机型加了约束。目前先不搞UI所以先白板，**此处留坑等以后来补。**

## info.plist
添加了两项：`UIStatusBarHidden`和`UIViewControllerBasedStatusBarAppearance`，但在目前的项目中名称上有些许变化，应该是版本更新带来的区别。  

两者都是对状态栏的隐藏（~~状态栏是指什么？~~ 状态栏`(UIStatusBar)`指iPhone/iPad/iPod屏幕顶部用于显示网络、时间和电量等的、高度为20点的控件。），但有区别：  

- `Status bar is initially hidden`：APP「启动」时的状态栏是否隐藏  

- `View controller-based status bar appearance`：APP「运行」时的状态栏是否隐藏  

- 参考：[[iOS]关于状态栏(UIStatusBar)的若干问题](http://www.cnblogs.com/alby/p/4859537.html)

# 2017.05.13 & 2017.05.14
## 新建group以及文件
1. 创建`Home/Controller`，以及Camera的group；
2. 创建文件`kiwiCam/kiwiCam/Home/Controller/HomeViewController`，并在`Main.storyboard`中的那个场景（scene）的class改成这个`HomeViewController`，给它添加一个`NavigationControllerScene`（好久不练手都忘了怎么添加了，找了一会才找到）。把之前的`ViewController`删掉。
    - **疑问：为啥要给home页添加一个`NavigationControllerScene`呢？**  
猜测：后续有功能需要用到。

> **一个困惑：**  
在目前的xcode中我只发现了新建group而没有新建文件夹，而这个group建立好了之后是不会在真正的项目的文件夹（finder）中显示出实体的，而如果直接在项目的文件夹中建立新文件夹又不会在xcode的工程项目的导航中显示（应该是因为没有关联上吧），所以要怎么搞才能使xcode项目导航的层次和真正的文件夹中的层次一致呢？

## Global文件夹
有一个桥接文件`Capture-Bridging-Header.h`，应该是因为项目使用了swift和oc两种语言。里面广告的部分就不管了，但还有「分享」（目前决定分享平台是QQ、微信和微博）和其他功能的部分，**现在先留个坑等回来填**，先不管oc的部分，把swift的部分搞清楚再说。

## 关于core data
~~上学期学了，忘了，再学一遍吧……~~
专门开了篇文章来翻译官网的[Core Data Programming Guide](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreData/index.html#//apple_ref/doc/uid/TP40001075-CH2-SW1)，翻完第一部分发现这个应用**似乎不需要用到Core Data啊**（Capture好像确实没用Core Data），所以暂时放一放。

# 2017.05.09
## 对开源项目Capture的分析
项目地址：[Capture](https://github.com/dulingkang/Capture)。一个一个group来分析好了：

0. 该项目是使用swift语言写的，我也打算用swift来写

1. 裁剪功能是使用的第三方提供的，语言是oc

2. Home中主要实现了主界面的view和controller

3. SeniorBeauty是选择好图片后的三个高级功能：模糊、贴图、滤镜；以及该界面相关的MVC（其实功能有四个，还有一个就是裁剪）

4. Camera是实现实时滤镜的，目前我不打算做这个功能，就直接调用自带的相机拍个照就可以了

5. Global，目前我的理解是定义了一些全局使用的view和model

6. Lib
    - OpenSource中应该是用来分享的接口
    - （百度广告就不提了）剩下**一堆framework，不知道是什么，查一查之后再来更新**

7. Util，应该是实用工具吧，但是**不知道那四个文件用来干嘛的，一样，查完搞清楚之后回来更新**

8. Resource里主要是用到的图片资源和info.plist。该项目基本没有使用storyboard，纯手工写view，我也打算这么写了

## 目前的计划
1. 这次就不作妖了，人家怎么写的就搞清楚之后自己写起来，不在大方向上随便瞎改了

2. 就从第一个commit开始看，一步步来写吧

-TBC-
