---
layout: post
title: "iOS逆向学习1-搭建移动渗透测试平台"
date: 2014-03-06 21:44:25 +0800
comments: true
categories: iOS
tags: iOS逆向学习
---
   本系列学习是基于对 [iOS安全系列汇总](http://esoftmobile.com/2014/02/14/ios-security/#jtss-tsina) 的学习与总结笔记。在此首先感谢各位作者！
   
   


[本文教材地址](http://wufawei.com/2013/11/ios-application-security-1/)(注：学习的话，请去教材那，有图有真相。赞一个 @)

<!--more--> 
## 一、越狱设备
  
  本人是iPod 5，7.0.6， 直接用[越狱工具](http://evasi0n.com/)，一次就越狱成功了，傻瓜式的，超简单（谁用谁知道）。
  
  大体流程：
  
  
  1. 下载运行evasion，它会自动检测设备，并判断是否可以越狱。   
  
  2. 点击jailbeak（越狱），waiting....
  
  3. evasion 自动重启设备，需要手动安装 已经出现在桌面上的 jailbreak 程序，静等，等设备重启后，看到一个Cydia的新app。越狱成功！
  
  
  注意：① 因为是小白，越狱前看了好多教程，大多都建议越狱前还原固件；② 胆子大 就可以了。
       
      
## 二、建立移动审计平台
 
 安装一些重要的命令行工具 - 审计iOS应用的工具。
 
 1. OpenSSH ：
 
  通过这个工具可以从Mac端登录到越狱设备。


【步骤】：

进入Cydia，点击底部搜索，输入：OpenSSH，安装即可。

2. BigBoss Recommendation tools：
	
据说所有流行的黑客工具都可以在此包中找到。

【步骤】：遇到了些小麻烦，直接在Cydia中搜索不到。解决方法，找到任意一个BigBoss 发布的包，查看更多此作者开发的包，Find it。


3. MobileTerminal

可以在设备上直接运行命令行，而不是通过ssh登陆设备运行。

【步骤】直接在Cydia 搜索MobileTerminal，安装。安装后，可以在桌面看到app图标，可输入任意unix命令测试。比如ps 列举正在运行的进程。

ps：通过ssh登陆越狱设备。

① 保证电脑与越狱设备在同一个网络，找到越狱设备ip地址（x.x.x.x）。

② 在电脑端 Terminal中 使用命令 ssh root @  x.x.x.x ,以root用户登陆进去。默认密码：alpine。
③ 安装好OpenSSH ，马上修改root默认密码。passwd ，输入两次新密码即可。

注意：ssh 使用root 登录时，Cydia 应在后台而不是前台。因为Cydia以root运行。

③ 获得最新的包列表 apt-get update.

4. class-dump-z

可以用它导出（dump） iOS应用的 类信息（classinfomation）。

【步骤】 ①得到其[官方地址](https://code.google.com/p/networkpx/wiki/class_dump_z),复制最新版本地址。

②ssh 进入设备，用 wget下载class-dump-z。

命令：wget http://networkpx.googlecode.com/files/class-dump-z_0.2a.tar.gz 

③ 使用tar 解压

tar -xvzf class-dump-z_0.2a.tar.gz 
④ 进入解压后的目录iPhone_armv6,然后复制class-dump-z的执行文件到 /usr/bin 目录。这样可以在设备上的任何目录都运行class-dump-z。

完成后 输入class-dump-z 测试查看安装成功。

## 三、总结
  
  1. 越狱设备
  
  2. 搭建审计平台-常用的审计工具
  
 
 
## PS：篇外


看到众多大神都搭建有自己的Blog 分享记录经验与成长，然早想记录有没有执行的我 揭竿而起，哈哈，风好的话，跟风无错哈。好好学习天天向上。

mardown 语法一窍不通。通过本文 熟悉了 几个格式：

① cmd + b 或者 XXstrongXX (X = *) or XstrongX  （X = _） eg： **strong** or __strong__ 

②连续回车（return）>=2 才是换行。否则在一行。

③ 超链接 使用 【链接名】（http://mrshyi.github # io）【】（）改成英文状态下。eg：[链接名](mrshyi.github.io)



----Continue--


