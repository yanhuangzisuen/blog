---
title: NSString的其他用法
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---

* 获取字符串的长度

```objc
- (NSUIntrger)length;
```

* 获取具体位置的字符

```objc
- (unichar)characterAtIndex:(NSUInteger)index;
//返回 index 位置对应的字符, %c 输出
```

* 字符串和其他数据类型转换

```objc
//转为基本数据类型
- (double)doubleValue;
- (float)floatValue;
- (int)intValue;
...
//转为C语言字符串
- (char *)UTF8String;
```

* NSString去除空格

```objc
//去除所有空格, 字符串替换
[str strByReplaceingOccurrencesOfString:@" " withString:@""];

//去除首位空格
[str stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceCharacterSet]];
```
