---
layout: post
title: "用Octopress+Github搭建Blog(2)- 个性配置"
date: 2014-04-16 23:39:09 +0800
comments: true
categories: Tool
tags: Octopress
---
### 0.修改 `_config.yml`文件
格式：`配置项：+ 空格 + 参数`，空格必选有，不能少。
<!--more-->
### 1.设置文章摘要显示

在正在编辑的`markdown`文件的摘要部分下面加上 `<!--more->` 即可。

要是想修改 `Read on`,则在 **_config.yml** 文件中 找到 `exerpt_link: "Read on &rarr;"` 修改成自己想要的文字。

### 2.主页显示文章数量设定

在 **_config.yml**文件中修改 `paginate` 至 自己想要的展示数量即可。

**翻页**，页面下方的**Older** 和 **Newer** 按键，可以通过，修改 **index.html **总对应内容。





---
###参考及引用
[Octopress文章摘要显示和主页显示文章数量设定](http://blog.csdn.net/hankai1024/article/details/12850413)

**lslin** [Octopress 个性配置汇总](http://blog.lessfun.com/blog/2013/12/05/config-the-octopress-blog-after-deployed/)
