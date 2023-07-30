---
layout: post
title: "A doubt about git"
date: 2014-05-30 15:33:32 +0800
comments: true
categories: Tool
tags: Git
---


    bug 分支     -bug修复
    master 分支  -稳定版
    dev 分支     -开发版
<!--more--> 
 当 出现bug时，
 
 	1.挂起 git stash dev 分支
 
 	2.从master分支上 分出 bug 分支
 
	3.修复bug，合并到 master 分支
 
 	4.恢复 dev 分支，git stash pop
 
 	5.把dev 合并到 master
 
 Q: dev 与 master 合并 merge 会因 bug分支出问题吗？
 
 验证：


 结论：
 
 若没有conflick，则不会出问题，正如两条普通分支meger 一样

