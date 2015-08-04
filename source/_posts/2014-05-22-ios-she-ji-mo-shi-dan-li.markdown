---
layout: post
title: "iOS 设计模式-单例"
date: 2014-05-22 21:35:11 +0800
comments: true
categories: 
---
	1.什么是单例
	2.应用场景
	3.如何实现与使用
	4.单例工厂
	5.模块管理
	
<!--more-->
# iOS 单例

### 1.什么是单例?

　　 是一个类在系统中只有一个实例对象。通过全局的一个入口对这个实例对象进行访问。

## 2.应用场景？  

　　用于只希望一个类只有一个实例，而不运行一个类还有两个以上的实例。

　　 **A:**iOS SDK 应用到单例模式的类:

　　 UIApplication 的 shareApplication 统一管理、  

　　 NSUserDefaults 的standardUserDefaults统一管理用户配置文件、  

　　 NSFileManager的defaultManager统一负责物理文件的管理、    

　　 NSNoficationCenter中defaultCenter负责全局的消息分发。  

　　**B:**定制场景：主题管理、下载管理、传递Data。

## 3.如何实现与使用？

ARC + GCD 实现 

xx.h

	+ (ARCSingleton *)sharedInstance;
xx.m

	+ (ARCSingleton *) sharedInstance
	{
		// 1
		static  ARCSingleton *sharedInstance = nil ;
		// 2
		static  dispatch_once_t onceToken;  // 锁
	 	// 3
		dispatch_once (&onceToken, ^ {     // 最多调用一次
			sharedInstance = [[self  alloc] init];
		});
		
		return  sharedInstance;
	}

	// 当第一次使用这个单例时，会调用这个init方法。
	- (id)init
	{
    	self = [super init];
    	if (self) {
        // 通常在这里做一些相关的初始化任务
    	}
		return self;
	}

1. 声明一个静态变量去保存类的实例，确保它在类中的全局可用性

2. 声明一个静态变量`dispatch_once_t`,它确保初始化器代码只执行一次

3. 使用`Grand Central Dispatch(GCD)`执行初始化的`block`.这正是单例模式的**关键**：一旦类已经被初始化，初始化器永远不会再被调用。

## 4.单例工厂  

　　管理项目中大量的单例  

　　工厂方法模式的实质是“定义一个创建对象的接口，但让实现这个接口的类来决定实例化哪个类。工厂方法让类的实例化推迟到子类中进行。”

## 5.模块管理系统

　　 统一管理


## 参考

1.iOS设计模式反思之单例模式的进化 http://blog.jobbole.com/56439/

2.iOS设计模式(02):单例模式 http://beyondvincent.com/blog/2013/05/09/20/