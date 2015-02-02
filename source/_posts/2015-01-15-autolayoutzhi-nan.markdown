---
layout: post
title: "Autolayout指南"
date: 2015-01-15 11:57:36 +0800
comments: true
categories: 
---

#简介

Autolayout通过各个控件之间创建数学描述关系来布局app的界面,在单个或者多个控件之间定义constraints联系,使用Auto layout,你可以创建动态自适应的用户界面来响应屏幕大小,设备横竖屏和本地化的变化

- 通过可视化Menu菜单添加constraints
- 通过代码添加constraints

##constraints基础

###什么是constraints
你可能想完成"视图button离父视图坐标相距20个像素",那么表达式可以写成button.left = container.left+20类似表达式y=m*x+b

- y和x是视图的attribute
- m和b是floating point值

以后constraints会遇到的attribute列表:

- left
- right
- top
- bottom
- leading
- trailing
- width
- height
- centerX
- centerY
- baseline

Constraints包含了其他的属性

- Constant Value: 偏移量
- Relation 与某个控件的位置关系
- Priority 优先级

#Interface Builder中操作Constraints

## Ctrl+Drag添加Constraints

添加Constraints最快的方式就是选中一个控件按住Ctrl键向某个方向(上下左右)拖动, 和我们创建控件链接到IBOutlets和IBAction的方式差不多

Ctrl+拖动某个控件就可以创建一个Constraints
