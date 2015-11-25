---
layout: post
title: "初识HTML"
date: 2014-04-16 21:54:24 +0800
comments: true
categories: FE
tags: html
---

## 写在前面
说是初识，其实已经是老相识了。记得n年前，还在学校的时候，开了一门web **的课程 ，对这些tag有印象，可惜当时不知忙什么了荒废的特别彻底，真是书到用时方恨少。现在“重温”那些相识却不相识的HTML吧。Fighting！
<!--more-->
## 什么是HTML
HTML 是用来描述网页的一种语言。

* HTML 指的是超文本标记语言（Hyper Text Markup Language）
* HTML 不是一种编程语言，而是一种标记语言（Markup Language）
* 标记语言是一套标记标签（markup tag）
* HTML 使用标记标签来描述网页

---

## HTML标签
HTML 标记标签通常被称为 HTML 标签（HTML tag）.

- HTML 标签是由尖括号包围的关键词，比如`<html>`

- HTML 标签通常是成对出现的，比如`<b></b>`
- 标签对中的第一个标签是开始标签，第二个标签是结束标签
- 开始和结束标签也被成为开放标签 和 闭合标签

---

## HTML 文档 ＝ 网页
* HTML 文档描述网页
* HTML 文档包含 HTML 标签和纯文本
* HTML 文档也被称为网页



Web 浏览器的作用是读取HTML 文档，比以网页的形式显示出它们。浏览器不会显示HTML 标签，而是使用标签来解释页面的内容

	<html>
	<body>
	<h1>My first Heading </h1>
	<p>My first paragraph.</p>
	</body>
	</html>  
例子解释

* 	`<html>` 与 `</html>` 之间的文本描述网页
* 	`<body>` 与 `</body>` 之间的文本是可见的页面内容
* 	`<h1>` 与 `</h1>` 之间的文本被显示为标题
* 	`p`与`/p` 之间的文本被显示为段落


## 参考文档

W3Scholl 的 [ HTML 简介](http://www.w3school.com.cn/html/html_intro.asp)

---
## 写在后面

小小一个简介，没什么内容，但由于不熟悉 markdown语言 ，编辑的超慢，而且是看着 W3Scholl的学习文档。这样的效率一晚上没了。坑。改变策略，一次多学点。记录简单的、有不同意义的知识点。然后抽时间 阶段总结。
***

`markdown`语法学习：

**Unordered Lists**
 
1使用` * + 空格` 或者`- + 空格` 可以生成：
 
 * 像我一样
 * 和我一样
 * 哈哈
 
2 使用  `` 在英文输入法下  ~ 这个键 两个之间 可以生成 ：
 
 `我` 
 还有 `<html>`

3 使用 三个* 或者三个- 或者 四个- 可以生成：
***
---
----

4 在行首 使用 Tab 键 或者 至少4给空格 可以生成：

	Tab
	你
	
    四个空格	


