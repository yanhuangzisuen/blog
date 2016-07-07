---
title: NSDictionary简写与文件操作
date: 2016-07-07 11:39:06
tags: NSDictionary
categories : "Objective-C"
---

## NSDictionary 的简写形式

* NSDictionary 的创建

```objc
//以前
[NSDictionary dictionaryWithObjectsAndKeys:@"Jack", @"name", @"男", @"sex", nil];

//现在
@{@"name" : @"Jack", @"sex" : @"男"};
```

* NSDictionary 获取元素

```objc
//以前
[dict objectForKey:@"name"];

//现在
dict[@"name"];
```

## NSDictionary 的文件操作

```objc
//写入文件
- (BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile;
- (BOOL)writeToURL:(NSURL *)url atomically:(BOOL)atomically;

//从文件中读取
+ (NSDictionary *)dictionaryWithContentsOfFile:(NSString *)path;
+ (NSDictionary *)dictionaryWithContentsOfURL:(NSURL *)url;
- (NSDictionary *)initWithContentsOfFile:(NSString *)path;
- (NSDictionary *)initWithContentsOfURL:(NSURL *)url;
```
