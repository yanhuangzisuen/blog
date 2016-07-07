---
title: Objective-C简介
date: 2016-07-07 11:39:06
tags: Objective-C
categories : "Objective-C"
---
## 简介

>OC是在C语言的基础上加了一些新的面向对象的语法, 将C语言的复杂的, 比较繁琐的语法封装的更为简单.完全兼容C语言, 也就是说在OC语言中可以写任意的C代码.

##发展史

* 20世纪80年代初期, `Brad Cox`结合了C语言和SmallTalk的优势, 设计出了Objective-C语言.

* 1985年, `乔布斯`创建了NeXT公司, 使用Objective-C开发用户界面包.

* 1995年, NeXT得到Objective-C的全部版权.

* 1996年, 苹果收购NeXT, NextStep更名`Cocoa`, OC成为开发运行在Mac平台上的软件的主力语言.

在苹果发布iOS系统之后, OC又成为了开发iOS程序的语言

##OC与C差异

* 源文件

扩张名 | 含义
:------------: | :-------------:
.h | 头文件
.c | C语言源文件
.cpp .cc | C++语言的源文件
.m | Objective-C语言源文件
.mm | Objective-C++语言源文件

* 数据类型

C中的数据类型:
![C数据类型](/img/C语言数据类型.jpg)

OC中的新增的数据类型:

类型 | 描述
:------------: | :-------------:
BOOL | 字面常量值, `YES`or`NO`
NSObject * | OC中的对象类型
id | 动态对象类型, 万能指针
SEL | 选择器数据类型
block | 代码块数据类型

* 关键字

    C语言关键字
```c
auto double int struct break else long switch case enum
register typedef char extern return union const float
short unsigned continue for signed void default goto
sizeof volatile do if while static
```
    OC新增关键字
```objc
@interface @implementation @end @public @protected
@private @selector @try @ catch @throw @finally
@protocol @optional @required @class @property @synthesize
@dynamic BOOL Class SEL YES NO id self super nil atomic
nonatomic retain assign copy block _
```
    OC中新增异常捕捉方法
```objc
@try {
    //可能出错的代码
}
@catch (NSException *exception) {
    //一旦出错可以补救的代码
}
@finally {
    //无论出错与否都会执行的代码
}
```
##OC面向对象编程的四个主要特征
* 抽象性
* 封装性
* 多态性
* 继承性
