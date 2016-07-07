---
title: NSDictionary
date: 2016-07-07 11:39:06
tags: NSDictionary
categories : "Objective-C"
---

    1. 字典, 通过一个 key 可以找到对应的 value
    2. NSDictionary 是不可变的, 一旦初始化完毕, 里面的内容就无法改变

## NSDictionary 的创建

```objc
+ (instancetype)dictionary;
+ (instancetype)dictionaryWithObject:(id)object forKey:(id <NSCopying>)key;
+ (instancetype)dictionaryWithObjectsAndKeys:(id)firstObject, ...;
+ (id)dictionaryWithContentsOfFile:(NSString *)path;
+ (id)dictionaryWithContentsOfURL:(NSURL *)url;
```


