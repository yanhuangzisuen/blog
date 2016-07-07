---
title: NSArray读写文件
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

* 将NSArray数据写入到文件中

```objc
NSArray *array = @[@"a", @"b"];

BOOL res = [array writeToFile:@"/Users/yan/Desktop/test.txt" atomically:YES];
```

* 从文件中读取数据到NSArray中

```objc
NSArray *array = [NSArray arrayWithContentsOfFile:@"/Users/yan/Desktop/test.txt"];
```
