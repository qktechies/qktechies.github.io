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
一个代表模块本身的对象

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

###项目环境设置
```
|___my-project
	|__node_modules
	|	|__grunt
	|__Gruntfile.js
	|__package.json
```

- package.json
包描述文件,包含模块所有的元数据:名字,版本,描述,作者

```
>npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (my-project)
version: (1.0.0)
description: my-project demo
entry point: (Gruntfile.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to /Users/qkong/Documents/demo_code/my-project/package.json:

{
  "name": "my-project",
  "version": "1.0.0",
  "description": "my-project demo",
  "main": "Gruntfile.js",
  "dependencies": {
    "grunt": "^0.4.5"
  },
  "devDependencies": {},
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

####dependencies属性
一般github是不会上传node_modules的文件,我们必须安装所需的包,运行
npm install(后面不跟包名)上,npm会查询当前目录下的package.json并解析它,所有在dependencies的包都会被安装,

npm install grunt --save会自动加入dependencies的版本信息

npm install grunt --save-dev会自动加入devDependencies的版本信息

区别是:--save-dev一般用于测试框架mocha等等,一般部署到服务器上时,不带有node_modules文件夹,可能有模块不同系统不兼容的问题,所以需要npm install安装所有dependencies中包括的所有包信息,而devDependencies只是用于平时开发测试,服务器上是不需要的

####version版本
版本格式MAJOR.MINOR.PATCH 例如"version": "1.0.0"
MAJOR 不兼容的API发布
MINOR 向后兼容的功能发布
PATCH 向后兼容的bug修复

- Gruntfile.js

npm是寻找当前目录的package.json
而grunt是寻找当前目录下的Gruntfile.js

内部代码都类似:

```
module.exports = function(grunt) {   // Do grunt-related things in here};
```


 



