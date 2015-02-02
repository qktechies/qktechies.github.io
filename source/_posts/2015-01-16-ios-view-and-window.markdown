---
layout: post
title: "ios view and window"
date: 2015-01-16 16:09:02 +0800
comments: true
categories: 
---

- 视图层级关系

![](https://developer.apple.com/library/ios/documentation/WindowsViews/Conceptual/ViewPG_iPhoneOS/Art/view-layer-store.jpg)

UIWindow:底部画板,持续存在与app整个生命周期内
app启动实例化UIApplicationMain
 UIWindow* w = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
 
设置window的rootViewController

- Super view和subview概念

- 视图绘画方式

UIView用于展现内容,

1. view第一次出现在屏幕上是,系统绘制它的内容并保留该内容的快照,视图再次加载并且没有变化,快照图片会被再次使用
2. 只有当视图内容发生变化,系统才会重新绘制该图片