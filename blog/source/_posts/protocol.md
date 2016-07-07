---
title: Protocol
date: 2016-07-07 11:39:06
tags: Protocol
categories : "Objective-C"
---

## 1、什么是Protocol?
 * 1）Protocol中文意思：协议。
 * 2）协议中只能声明一些方法。
 * 3）遵守了协议，就等于拥有了协议中的所有方法。

## 2、协议的基本用法：
 * 1、协议的定义格式：
```objc
  @protocol 协议名称
  // 各种方法；
  @end
 ```
 * 2、协议的使用格式：
```objc
 @interface 类名 : NSObject <协议名1，协议名2，...>
 @end
 ```

## protocol的使用注意

 * 1）把同一类方法，放到1个协议当中
 * 2）1个类可以同时遵守多个协议。
 * 3）父类遵守了某个协议，子类也遵守了该协议。
 * 4）协议遵守协议：1个协议可以遵守多个协议。

## protocol基协议介绍
 ```objc
@protocol SportProtocol <NSObject>
@end

 * 此处的NSObject就是基协议，意义等同于继承NSObject。
 * 继承基协议的好处：能够拥有基协议当中所声明的所有方法。
```
* 总结：
* 1、需要添加成员变量和方法时，建议使用继承
* 2、只需要添加方法时，建议使用分类
* 3、当很多不同类中，有共同的方法可以抽取时，类之间不存在继承关系，建议使用协议。


## protocol中@required和@optional
* @required：用@required修饰的方法，必须实现。
* @optional：用@optional修饰的方法，可实现，可不实现。
* @required 和 @optional的主要意义:一般用于序员交流用。
