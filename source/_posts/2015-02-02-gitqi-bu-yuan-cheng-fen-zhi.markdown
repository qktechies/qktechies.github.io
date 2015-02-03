---
layout: post
title: "git起步4-远程分支"
date: 2015-02-02 16:32:19 +0800
comments: true
categories: 
---

远程分支是远程仓库中分支状态的指针,他们是本地不能移动的分支

格式(remote)/(branch)

##查看所有的远程

```
$ git remote -v
origin	https://github.com/schacon/simplegit-progit (fetch)
origin	https://github.com/schacon/simplegit-progit (push)
```

默认origin,例如有人开了一个iss53分支纠正bug,那么你申请修改bug时,可以把修改完的代码提交到origin/iss53

origin不是特殊的:
就像分支master是git目录起始的默认分支名,origin也是git从远程传clone下来后的远程仓库

团队开发有个git.ourcompany.com的git服务器,git clone:

- 命名远程仓库为origin,下载所有的数据
- 建立一个指向它的master分支指针,在本地命名为origin/master,你无法修改其数据
- 建立属于自己的本地master分支,在这个分支上工作

![](/images/gitqi-bu4/1.png)

如果有人将他的更新代码提交到服务器git.ourcompany.com上并更新了它的master分支,而我们也在本地修改了代码,此时我们本地的origin/master指针不会移动

![](/images/gitqi-bu4/2.png)

为了同步工作,必须先运行git fetch origin从服务器上拉取没有的数据

![](/images/gitqi-bu4/3.png)

当多个团队开发时,服务器处于git.team1.ourcompany.com,你可以使用git remote add [url]添加远程仓库

![](/images/gitqi-bu4/4.png)

git fetch teamone可以拉取teamone服务器中本地没有的消息,origin/master中包含了teamone/master的所有checksum,所以没有拉取数据而是设置了一个远程分支名为teamone/master

![](/images/gitqi-bu4/5.png)

