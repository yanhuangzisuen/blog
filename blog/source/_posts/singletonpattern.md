---
title: 单例模式
date: 2016-07-07 11:39:06
tags: 单例模式
categories : "Objective-C"
---

#### 1、单例模式概念
* 1、 什么是单例模式:(Singleton)
 * 单例模式的意图是的类的对象成为系统中唯一的实例,提供一个访问点,供客户类共享资源。

* 2、 什么情况下使用单例?
 * 1）类只能有一个实例,而且必须从一个为人熟知的访问点对其进行访问,比如工厂方法。
 * 2）这个唯一的实例只能通过子类化进行扩展,而且扩展的对象不会破坏客户端代码。

* 3、 单例设计模式的要点:
 * 1）某个类只能有一个实例。
 * 2）他必须自行创建这个对象
 * 3）必须自行向整个系统提供这个实例;
 * 4）为了保证实例的唯一性,我们必须将如下方法实现进行覆盖
```objc
-(id)copyWithZone:(NSZone *)zone +(id)allocWithZone:(NSZone *)zone -(id)retain -(NSUInteger)retainCount
-(oneway void)release
-(id)autorelease 。
```
 * 5）这个方法必须是一个静态类。
* 4、 在OC中实现单例模式:
```objc
先创建一个单例类,即:
#import <Foundation/Foundation.h>
@interface Bee : NSObject<NSCopying>//注意此处调用了NScoping协议
+ (Bee *)shareIsrance;//此处定义了一个工厂方法,用工厂方法来限制实例化过程
@end //调用NScoping协议,从而在实现文件中覆盖
```

#### 简单的单例模式实现

```objc
//Tools.h文件

#import <Foundation/Foundation.h>

@interface Tools : NSObject <NSCopying, NSMutableCopying>
//一般情况下,创建一个单例对象都会提供一个类工厂方法
//一般情况下,用于创建单例对象的方法名都以 share 开头或 default 开头
// share + 当前的类名
+ (instancetype)shareTools;//仅仅是提供一个 share 的类方法,无其他意义
@end
```

```objc
//Tools.m文件

#import "Tools.h"
@implementation Tools

+ (instancetype)shareTools
{
    Tools *instance = [[self alloc] init];
    return instance;;
}

static Tools *_instance = nil;//1.定义一个全局变量

+ (instancetype)allocWithZone:(struct _NSZone *)zone
{
//    多线程可能有问题
//    2.由于所有的创建方法都会调用该方法,所以只需要在该方法中控制当前对象只创建一次
    /*
    if (_instance == nil) {
        _instance = [[super allocWithZone:zone] init];
    }
    return _instance;
     */
//    以下在多线程也没有问题 保证在多线程也执行一次  GCD
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        _instance = [[super allocWithZone:zone] init];
    });
    return _instance;
}
//  3.重写 copy
- (id)copyWithZone:(NSZone *)zone
{
    return _instance;
}

- (id)mutableCopyWithZone:(NSZone *)zone
{
    return _instance;
}

// MRC 中的单例要重写以下方法
- (oneway void)release
{
//    为了保证整个程序过程中只有一份实例,在这个方法中什么都不做
}

- (instancetype)retain
{
    return _instance;
}

- (NSUInteger)retainCount
{
//    return 1;
//    注意:为了方便沟通,一般情况下,单例中不会返回 retainCount = 1;
//    一般返回比较大的值
    return NSUIntegerMax;
}
```
