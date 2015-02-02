---
layout: post
title: "file and directory permissions"
date: 2015-01-26 10:05:44 +0800
comments: true
categories: 
---

####users of file
- the owner(the process' UID matcheds the user of the file)
- the group(the process' GID is a member of the file's group)
- the other(everyone else)

####用户三种权限:
- read
- write
- execute

permissions assigned to a directory are not inherited by the files within that directory
文件不继承上层目录的权限

####目录权限:
- read: list the files in a directory(ls)
- write: add a file to the directory, delete a file from a directory, rename a file
- execute: cd into it(make some directory your current working directory), access the "inode" information of the files within

目录有两个属性:名字和inode号
read可以获取文件名
execute可以获取文件inode号

"cat /home/user/foo"需要文件foo的读权限
只有你拥有/,/home,/home/user的搜索权限时,cat才能获取到foo文件的inode并且读取其中的内容,只有搜索到文件的inode才能读取其中的内容


####细节
每个文件和目录有12个可设置的权限,意味着有2^12=4096中可能的权限设置,12bits要么on要么off,每个权限可以独立被修改.

文件权限和属性信息保存在文件inode中,只有文件的属主可以修改文件的inode例如permission和group.
文件owner修改permission不需要任何权限
只有root用户才能修改文件的owner

permission没有赋予用户权利运行某些程序,而是赋予权利运行某些system call(UNIX API)
例如:cat和more都使用了read() system call


除了9位权限位(rwx for owner, group and others),还有三位:

- set User ID(SUID or setuid)
- set Group ID(SGID or setgid)
- sticky(or text) bit

####Files

用户尝试使用unix命令例如cat读文件内容时,system call read()将会被调用并且"r" permission is required. 系统检查用户是不是属主并且属主有没有"r" permission,如果不是,系统检查用户是不是文件属组中一员,如果以上都不是,那么查看others是否被赋予了"r" permission


####执行权限和脚本
如果用户有某个文件的"x" permission而没有"r" permission,他就可以执行这个文件, 但他不能copy文件
