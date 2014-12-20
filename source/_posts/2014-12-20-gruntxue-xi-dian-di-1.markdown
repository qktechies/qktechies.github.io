---
layout: post
title: "Grunt学习点滴1"
date: 2014-12-20 12:10:49 +0800
comments: true
categories: 
---

#Grunt是基于nodejs的javascript命令行工具

##在学习grunt之前必须知道:

###nodejs
官网下载安装[http://www.nodejs.org/download/](http://www.nodejs.org/download/)

查看是否安装成功:

```
$node --version
v0.10.33

$npm --version
1.4.28
```
###Modules

nodejs模块化是CommonJS规范的实现,因为原生的javascript没有这个特性,相当于JAVA中的import

Commonjs的说明:[http://wiki.commonjs.org/wiki/CommonJS](http://wiki.commonjs.org/wiki/CommonJS)

三个重要的说明:

- ####module
一个代表模块本生的对象

- ####exports
提供对外访问的接口,利用require可以得到exports对象

- ####require
用于import模块,返回exports对象

```
//三个文件index.js,increment.js,math.js
//program.js
var inc = require('./increment').increment; 
var a = 1;console.log(inc(a));
//increment.jsvar add = require('./math').add; 
exports.increment = function(b) {       return add(b, 1);};
   //math.jsexports.add = function(c, d) {       return c + d;};
```
increment.js对外提供increment接口,通过调用math中add接口实现自增1

math.js对外提供add接口

运行结果:

```
$node program.js
 2
```

CommonJS利用了计算机科学抽象的思想,例如increment.js调用math.js中的add接口时,不需要知道add的实现细节,只需要写math.js的人告诉它:add接口实现了两个数相加的方法

这样我们可以把实现特定方法的函数写在多个模块文件中,提高代码复用率

###npm(Node Package Manager)
nodejs包管理器

##Grunt
###安装Command-line interface(CLI)

```
$npm install -g grunt-cli
```

在项目中使用grunt之前,我们先安装grunt

```
$cd my-project
$npm install grunt
```

###项目的设置
- package.json
- Gruntfile.js


 



