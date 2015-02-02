---
layout: post
title: "ios设计模式"
date: 2015-01-12 10:16:26 +0800
comments: true
categories: 
---

###Using Design Patterns 设计模式

- MVC
Model-View-Controller

Model:记录app的数据

View:现实用户界面,填充app内容

Controller:控制视图,模型和视图交流的渠道

![](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/Art/ModelViewController_2x.png)

ToDoList app中:

storyboard:视图

AddToDoItemViewController:控制器

- Target-Action(目标动作模式)

![](https://developer.apple.com/library/ios/referencelibrary/GettingStarted/RoadMapiOS/Art/target_action_2x.png)

按下某个按钮时,调用click方法,此时target就是按钮对象,action是controller中的click方法

- Delegation 代理模式


###Foundation

- Value Objects

NSString和NSMutableString

NSData和NSMutableData

NSDate

NSNumber

NSValue

- Strings - NSString

- Numbers - NSNumber 

- Collection Objects

NSArray和NSMutableArray

NSSet和NSMutableSet

NSDictionary和NSMutableDictionary


