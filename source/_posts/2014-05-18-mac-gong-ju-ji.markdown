---
layout: post
title: "Mac 工具集"
date: 2014-05-18 15:37:57 +0800
comments: true
categories: iOS
tags: iOS逆向学习
---
目录
	
	1.class-dump
	2.Theos
	3.Reveal
	4.IDA
	5.Other
<!--more-->
### 1. class-dump
   class-dump,顾名思义,就是用来 dump 目标对象的 class 信息的工具。它利用 Objective-C语言的 runtime 特性,将存储在 Mach-O 文件中的 @interface 和 @protocol 信息提取出来,并 生成对应的 .h 文件。 
   
    
  [下载地址](http://stevenygard.com/projects/class-dump/)
 选择 class-dump-3.5.dmg 下载后,将 dmg 文件中的 class-dump 复制到 /usr/bin 目录,并 在 Terminal 中执行“ ’sudo chmod 777 /usr/bin/class-dump‘”命令赋予其执行权限,然后运行class-dump 。

### 2.Theos

### 3.Reveal

### 4.IDA

### 5.Other 







---
###主要参考

图书： [《iOS逆向工程》](http://iosre.com/)

BBS:  [iOS Reverse Engineering](http://bbs.iosre.com/)