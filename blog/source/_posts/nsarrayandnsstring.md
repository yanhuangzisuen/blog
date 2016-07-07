---
title: NSArray与NSString
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

* 将数组元素连接成字符串

```objc
//NSArray的方法
//用 separator 作为拼接符将数组元素拼接成一个字符串
- (NSString)componentsJoinedByString:(NSString *)separator;
```

* 将字符串分割成一个数组

```objc
//NSString的方法
// 将字符串用separator作为分隔符切割成数组元素
- (NSArray *)componentsSeparatedByString:(NSString *)separator;
```
