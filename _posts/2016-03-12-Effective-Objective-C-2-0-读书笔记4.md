title: Effective Objective-C 2.0 读书笔记4
date: 2016-03-12 23:40:21
comments: true
categories: [iOS]
tags: [iOS,Objective-C,Effective]
---
### 第11条：理解objc_msgSend的作用
* **动态绑定** ，调用函数直到运行期确定
* 给对象发送消息 
	* id returnValue = [someObject messageName:parameter]; 
	* 转换函数 void objc_msgSend(id self,SEL cmd,...)
	* id returnValue = objc_msgSend(someObject,@selector(messageName:),parameter);
* 特殊情况的消息调用
	* objc_msgSend_stret 待发送的消息要返回结构体
	* objc_msgSend_fpret 消息返回的时浮点数
	* objc_msgSendSuper 要给超类发送消息
* **尾调用优化** (tail-call optimization) 若函数最后一项操作是调用另外一个函数，运用此技术，编译器会生成调转至另一函数所需的指令码，而不会向调用堆栈中推入新的“栈帧”。只有当函数最后一项操作仅仅时调用其他函数而不会将其返回值另作他用时，才会执行“尾调用优化”。
	
<!--more-->
---
**要点**

* 消息由接收者、选择器及参数构成。给某对象“发送消息”(invoke a message),也相当于在该对象上“调用方法”（call a method）
* 发给某对象的全部消息都要由“动态消息派发系统”（dynamic message dispatch system）处理，该系统会查出对应的方法，并执行其代码

### 第12条：理解消息转发机制
  对象在收到无法解读的消息后，会启动“消息转发”（message forwarding）
  
消息转发的两大阶段

* 第一阶段先征询接收者，所属的类，看其是否能动态添加方法，以处理当前这个“未知的选择器”（unknown selector），成为“动态方法解析”。
* 第二阶段涉及“完整的消息转发机制”（第一阶段执行完后，接收者无法再以动态新值方法手段响应包含该选择器的消息）
	* 请求接收者看看有没有其他对象以其他对象能处理这条消息，有则转给那个对象，消息转发过程结束，一切如常；无“备援接收者”（replacement receiver）则启动完整消息转发机制，消息相关细节被封装到NSInvocation对象中

#### 动态方法解析
对象在接收到无法解读的消息后，首先调用其所属类的方法

 `+(BOOL) resolveInstanceMethod:(SEL)selector` 

或者

 `+(BOOL) resolveClassMethod:(SEL)`，

参数为未知消息的选择器，返回值表示是否能新增一个实例方法用以处理此选择器

前提：相关方法的实现代码已经写好，只等运行时动态插入类中

#### 备援接收者

当前接收者第二次机会能处理未知的选择器，这一步中，运行期系统询问能否把这条消息转给其他接收者来处理：

`-(id) forwardingTargetForSelector:(SEL)selector`

参数为未知的选择器，若能找到备援对象，将其返回，若找不到，返回nil

注：无法操作经由这一步转发的消息，若要在转发之前修改消息内容，需通过完整的消息转发机制

#### 完整的消息转发

若转发算法到此步骤，只能启用完整的消息转发机制

* 首先创建NSInvocation对象，把与尚未处理的消息相关细节封装其中，包含选择器，目标及参数
* 触发NSInvocation对象时，“消息派发系统”（message-dispatch system）把消息指派给目标对象

`-（void) forwardInvocation:(NSInvocation*)invocation`

改变调用目标，使消息在新目标上调用，若发现不应由本类处理，则调用超类同名方法

#### 消息转发全流程

流程图

接收者在每一步均有机会处理消息。步骤越往后，处理代价越大。

---
**要点**

* 若对象无法响应某个选择器，则进入消息转发流程
* 通过运行时的动态方法解析功能，可以在需要用到某个方法时再将其加入类中
* 对象可以把其无法解读的某些选择器转交给其他对象处理
* 经由以上步骤无法处理，则启动完整的消息转发机制

### 第13条：用“方法调配技术”调试“黑盒”方法

**方法调配**（method swizzling）给定选择器名称的对应方法在运行期改变，新功能将在本类的所有实例方法中生效

类的方法列表会把选择器名称映射到相关的方法实现之上，使得“动态消息派发系统”能根据此找到应该调用的方法。方法以函数指针的形式表示，叫IMP，`id (*IMP) (id ,SEL,...)`

Objective-C 运行期系统提供的几个方法都能操作上表。

* 新增选择器，
* 改变选择器对应方法的实现
* 交换选择器所映射到的指针
	* 交换方法实现`void method_exchangeImplementations(Mehod m1,Mehod m2)`
	* 获取方法实现`Method class_getInstanceMethod(Class aClass,SEL aSelector)`

---
**要点**

* 在运行期，可以向类中新增或替换选择器所对应的方法实现
* 使用另一份实现来替换原有方法实现，叫做“方法调配”，可用于向原有实现中添加新功能
* 通常，只有调试程序的时候才需要在运行期修改方法的实现，避免滥用

### 第14条：理解“类对象”的用意

**类型信息查询**（instrospection）在运行期检视对象类型

Objective-C 对象实例都是指向某块内存数据的指针，对象所需内存分配在堆上。

Object-C对象数据结构：

```objc
typedef struct objc_object {
	Class isa;//对象所属类（元类）
	Class super_class;//确立继承关系（超类）
} *id;
```
每个类仅有一个”类对象“，每个”类对象“仅有一个与之相关的”元类“

#### 在类继承体系中查询类型信息
可以用类型信息查询方法检视类继承体系。

* `isMemberOfClass:`判断对象是否为某个特定类的实例
* `isKindOfClass:` 判断对象是否为某类或其派生类的实例

类对象是”单例“，在应用程序范围内，每个类的Class仅有一个实例。

```objc
// 精确判断出对象是否是某类实例
id object = /*...*/;
if([object class] == [SomeClass class]){
	// 'Object' is an instance of SomeClass
}
```
Class 方法返回的类表示发起代理的对象，而非接受代理的对象

---
**要点**

* 每个实例都有一个指向Class对象的指针，用以表明其类型，而这些Class对象则构成类类的继承体系
* 如果对象类型无法在编译期确定，那么就应该使用类型信息查询方法来探知
* 尽量使用类型信息查询方法来确定对象类型，而不要直接比较类对象，因为某些对象可能实现类消息转发功能