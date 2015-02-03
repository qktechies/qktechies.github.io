---
layout: post
title: "head first servlet1"
date: 2015-01-31 10:31:01 +0800
comments: true
categories: 
---

- HTTP是Hypertext Transfer Protocol,位于TCP/IP上层Web网络协议
- Http使用request/response模型,客户端发起一个Http请求,web服务器返回一个Http response
- Http request包括:
  
  请求URL
  
  http方法(GET,POST等等)
  
  可选表单参数数据(query string)
- Http response包括:

  状态码(200,404)
  
  content-type(MIME值,text/html,application/json)
  
  实际response内容(HTML,图片等等)
  
- get请求把参数数据拼接到url后面
- post请求吧参数数据放在请求body里
- MIME值告诉浏览器数据类型(图片,声音,html),浏览器根据数据类型知道如何渲染它
- URL(Uniform Resource Locator) 统一资源定位符,网络上每个资源都有唯一的地址:

  http://121.30.50.60:90/2013/4/demo.png
  
  http://:protocol协议名
  
  121.30.50.60: 服务器名
  
  90: 端口号
  
  2013/4: 路径
  
  demo.png: 资源名称
- web服务器擅长于静态html界面,如果你需要在页面上动态加载数据,你就需要其他的app来帮助你,非Java类Perl就用CGI(Common Gateway Interface)
- 把html界面放在out.println()中不易于维护,jsp解决了这个问题,可以再html界面中加入java


