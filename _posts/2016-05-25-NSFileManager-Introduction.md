title: NSFileManager Introduction
date: 2016-05-25 20:54:55
comments: true
categories: [iOS]
tags: [iOS, Foundation]
---
## Introduction

![NSFileManager](http://7xonmx.com1.z0.glb.clouddn.com/NSFileManager.png "NSFileManager")

---
`NSFileManager` 对象查看（examine）和修改文件系统的内容。通常，我们和文件系统打交道，首次接触的就是它。我们用它来定位(locate)，创建(create),拷贝(copy)，移动(move)文件和目录。也通过它来获取文件或者目录的信息，改变它的一些属性（attributes）。

`NSFileManager` 类提供了一些便捷的方式来访问共享的文件管理对象，适用于大多数类型的文件操作。如果不打算直接使用它，例如，打算给它一个 delegate 对象，那么我们要创建这个类的实例。

我们可以用 `NSURL` 或 `NSString`对象，来指定文件的位置。当指定文件系统项时，我们优先使用 `NSURL` 类，因为它们可以将路径信息转换成更有效的表示法。

在我们移动，拷贝，连接或删除文件或目录时，我们可以用 delegate 结合文件管理对象来管理那些操作。delegate负责去确定(affirm)操作和决定发生错误的时候是否继续。在 OSX v10.7 和之后，delegate 必须遵守 `NSFileManagerDelegate` 协议。

在 iOS 5.0 及之后，OSX v10.7 及之后，`NSFileManager`包含了很多方法来管理存存在 `iCloud` 中的项。做了云存储标记的文件和目录会被同步到`iCloud`中，这样在用户的iOS设备和Mac上都可以使用它们,并且在一个地方修改，会传播到其他地方，以确保同步。

## Threding Considerations
`NSFileManager`对象共享的方法可以被多线程安全调用。然而我们用 delegate 来接收 移动，拷贝，删除，连接操作的状态通知时，我们需要创建唯一的文件管理对像实例，并把delegate赋给它，并用它来执行文件操作。