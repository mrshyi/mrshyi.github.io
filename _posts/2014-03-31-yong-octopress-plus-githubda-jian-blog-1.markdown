---
layout: post
title: "用Octopress+Github搭建Blog(1)"
date: 2014-03-31 22:36:47 +0800
comments: true
categories: Tool
tags: Octopress
---



## 1.搭建 Ruby 环境( Octopress 基于 Ruby环境 )，通过RVM 或者 Renvb （二者优缺点 各有所爱）。
   
   a.安装RVM：
     
     bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)
<!--more-->     
  
  b.配置classpath
  
  	echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile 
   
    source ~/.bash_profile
  c.安装 Ruby: (不明所以  不用  1.9.3 ？莫名其妙，用高版本也行，就是安装老出问题，囧)
    rvm install 1.9.3   
   
    rvm use 1.9.3
     
    rvm rubygems latest
   d.完成以上操作之后，运行验证， 看到 Ruby 1.9.3 则环境已经装好！
    ruby —version

    
   
## 2.安装 Octopress
   **注意**：安装之前，确认PC已经安装有git,在终端输入 git —version ，可以看到电脑中的git版本。若没有相关内容，先安装git。
   
   a.通过 git 命令将 Octopress 从 github 上 clone 到本机，命令如下：
   
     git clone git://github.com/imathis/octopress.git octopress
      
     cd octopress
   b.安装相关依赖项：（不太明白，有其他提示）
   
    gem install bundler
    bundler install
   c.安装默认主题
   
    rake install
    
    ps:安装Custom Theme：
    ① git clone git@github.com:shashankmehta/greyshade.git .themes/greyshade
     [可选：配套greyshade Theme]
        echo "\$greyshade: color;" >> sass/custom/_colors.scss     //Substitue 'color' with your highlight color
    ② rake install['greyshade’]
    
    
 d.配置 Octopress
    
   多数情况下，只需配置 _config.yml 和 Rakefile 文件即可。其中 Rakefile文件 跟Blog 部署有关，通常不需要修改，除非使用了 rsync。
   
   _config.yml 是Blog 重要的一个配置文件：有三大配置项：Main Config、 Jekyll & Plugins 和 3rd Party Settings。
    
   **建议**：删除 twitter 相关，否则，墙的原因，造成页面load 很慢。同理，修改 /source/_includes/custom/head.html 把google 的自定义字体去掉。

## 3.将 Blog 部署到GitHub上
   Github 的 Page sevice  可以免费托管博客，并且可以自定义域名。
  
a.在Github 上 创建一个仓库，并将仓库名称按照这样的方式命名：username.github.com 或者 organization.github.com.（配置完成之后，http://username.github.com 访问博客。博客源码 放到source分支，生成的内容提交到master 分支）
    
b.利用 Octopress 的 配置Rake 任务 自动配置上面创建的仓库，部署Github page：

    rake setup_github_pages
    (创建了一个_deploy 目录，存放部署到master分支的内容)
    根据提示输入仓库的url
    …………….
    
 C.生成Blog 并 部署到仓库中：
  
    rake generate // 可选
    rake preview // 预览 ，可选 (浏览器 本地查看 http://127.0.0.1:4000 或者http://localhost:4000)
    rake deploy    
    
   ps:上面的命令首先生成博客文件，并把生成的博客文件拷贝到_deploy/ 目录下，然后将这些内容添加到git 中，并将commit 和 push 到仓库的master分支。
    
  d.博客的source 需要单独提交，执行如下命令将source 提交到仓库的source分支下：
  
    git add .
    git commit -m ‘Initial source commit’
    git push origin source

## 4.写博客
  博文必须存储在 source/_posts 目录下，并按照Jekyll 命名规范对文章命名：YYYY-MM-DD-post-title.markdown。文章的名字会被当成url的一部分，而其中的日期用于对博文的区分和排序。
  
   创建博文：
   
    rake new_post[“title”]
   
   其中 title 为博文的文件名，默认markdown格式。命令生成这样的文件：source/_posts/2014-03-02-title.markdown.
   
   打开后，看到：(告诉Jekyll 博客引擎 如何处理博文和页面)
    
    —-------
    layout: post
    title: ”title”
    date: 2014-03-02 16:35
    comments: ture
    categories:
    ------
   我们在其中写我们的博客。完成后 预览和部署。

 写博客 到 发布 的完整流程：
 
 	 ① rake new_post["title”]    // 创建
	 ② rake generate             // 生成
     ③ rake preview			  //本地预览（可选）
     ④ git add .                 // 上传源文件（可选）
  	    git commit -am “commet “	
  	    git push origin source
     ⑤ rake deploy              // 部署 即 发布




---
---
## 待解决完善问题：

1.个性化配置：博客名、头像、主题、添加评论、域名解析、分享等。

2.不能直接使用 Rake xxx，必须使用 在之前加上  bundle exec 

3 对于文中所用的各种命令，一窍不通，只是比照着前辈大神们的教程。努力知其然，知其所以然。

4.关于Markdown 语法格式的学习：
	
	① --- 三个小短线 生成 如下的这种分界线；
	② 使用 # 来定义标题，按个数 从1到6 分别代表 一级标题 至 六级标题；
	③ 行的开头空4个空格，表示程序代码，如这些背景色比较重的地方。（Tab 这个看个人设置吧）
	
温故而知新：

	   单个回车   视为空格。

	   连续回车	 才能分段。

	   行尾加两个空格，这里->  即可段内换行。
	
分享一个 Markdown 的 [快速入门](http://www.ituring.com.cn/article/23)

---
本文是本人搭建 这个博客，实践过程与总结记录。

## 主要参考
 
[Octopress Documentation](http://octopress.org/docs/)

[@破船之家](http://beyondvincent.com/) 的 [利用Octopress搭建一个Github博客](http://beyondvincent.com/blog/2013/08/03/108-creating-a-github-blog-using-octopress/)

[@唐巧的技术博客](http://blog.devtang.com/)的[象写程序一样写博客：搭建基于github的博客](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/)

[812lcl](http://812lcl.com/) 的 [Octopress博客搭建及目录结构](http://812lcl.com/blog/2013/10/25/octopressbo-ke-da-jian-ji-mu-lu-jie-gou/)


