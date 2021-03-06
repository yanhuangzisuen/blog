---
title: protocol类型限制
date: 2016-07-07 11:39:06
tags: id
categories : "Objective-C"
---

## protocol类型限制

```objc
id d = [[Person alloc] init];

要求：变量d指向的对象必须遵守PlayProtocol协议
id<PlayProtocol> d = [[Person alloc] init];

要求：要求Person创建出来的对象，必须遵守PlayProtocol协议。
Person < PlayProtocol > *p = [[Person alloc] init];

真实使用场景:
@interface Person :NSObject <PlayProtocol>
@end
这样创建的任何对象，都拥有协议当中的方法。

```

## id和instancetype的区别

```objc
创建对象：
(id)person {
    return [[Person alloc] init];
}

这样，子类无法用这个方法创建对象：
(id)person {
    return [[self alloc] init];
}

调用自己没有的方法，程序会崩溃
建议使用：
(instanstype)person {
    return [[self alloc] init];
}

```
## 总结：
* id和instancetype的区别
 * 1）instancetype只能作为函数或者方法的返回值
 * 2）id能作为方法或者参数的数据类型、返回值，也能用来定义变量。
 * 3）instancetype对比id的好处：
    * 能精确的限制返回值的具体类型。
