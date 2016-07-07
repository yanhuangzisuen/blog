---
title: NSFileManager的文件访问
date: 2016-07-07 11:39:06
tags: NSFileManager
categories : "Objective-C"
---

## 获取文件\文件夹的属性

```objc
//获取文件\文件夹属性用法
- (NSDictionary *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error;
//eg:
//1.文件地址
NSString *filePath = @"/Users/yan/Desktop/test";
//2.获取文件管理者
NSFileManager *fileManager = [NSFileManager defaultManager];
//3.获取文件属性
NSDictionary *dic = [fileManager attributesOfItemAtPath:testPath error:nil];
NSLog(@"%@",dic);
```

## 获取某一个文件夹下的所有子路径

```objc
- (NSArray *)subpathsAtPath:(NSString *)path;
- (NSArray *)subpathsOfDirectoryAtPath:(NSString *)path error:(NSError **)error;
```

## 获取某一个文件夹下的当前子路径

```objc
- (NSArray *)contentsOfDirectoryAtPath:(NSString *)path error:(NSError **)error;
```

## 获取文件内容

```objc
- (NSData *)contentsAtPath:(NSString *)path;
```
