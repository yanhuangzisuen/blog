---
title: 为自定义的类实现copy操作
date: 2016-07-07 11:39:06
tags: Copy
categories : "Objective-C"
---

#####自定义对象copy步骤

* 新建Person类
* 为Person类实现copy操作
 * 1.让Person类遵守NSCopying协议
 * 2.实现 copyWithZone:方法,在该方法中返回一个对象的副本即可。
 * 3. 在copyWithZone方法中,创建一个新的对象,并设置该对象的数据与现有对象一致, 并返回该对象.

 * 创建Person对象, 调用copy方法, 查看地址。

* 细节介绍:
 * 1、 调用copy其实就是调用copyWithZone方法,所以要实现copyWithZone方法。(查看NSObject协议中的copy方法的介绍)
 * 2、 copyWithZone方法返回值类型是id类型,需要返回一个对象的副本。
 * 3、 关于copyWithZone的参数zone问题:
   *  zone: 表示空间,分配对象是需要内存空间的,如果指定了zone,就可以指定新建对象对应的内存空间。但是:zone是一个非常古老的技术,为了避免在堆中出现内存碎片而使用的。在今天的开发中,zone几乎可以忽略

   *  查看NSCopying协议中的allocWithZone:方法介绍(zone参数可以被忽略,是历史 原因)
  *  4、如果对象没有 可变/不可变 的版本区别,只要实现 copyWithZone 方法即可.

  *  5、copyWithZone:方法的具体实现:


```objc
- (id)copyWithZone:(NSZone *)zone{
//创建对象
Person *p1 = [[Person alloc] init]; //用当前对象值给新对象的实例变量赋值 p1.age = self.age;
//返回新对象
return p1;
}
```
* 为Person类实现mutableCopy操作
 * 1.遵守NSMutableCopying协议
 * 2.实现协议对你的方法

```objc
- (id)mutableCopyWithZone:(NSZone *)zone{
//创建对象
Person *p1 = [[Person alloc] init]; //用当前对象值给新对象的实例变量赋值 p1.age = self.age;
//返回新对象
return p1;
}
```
