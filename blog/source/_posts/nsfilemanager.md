---
title: NSFileManager
date: 2016-07-07 11:39:06
tags: NSFileManager
categories : "Objective-C"
---

1. NSFileManager 是用来管理文件系统的
2. 可以进行常见的文件, 文件夹操作
3. 使用了单例模式, [NSFileManager defaultManager] 获取单例

## NSFileManager 的常见用法

```objc
//判断文件或文件夹是否存在
- (BOOL)fileExistsAtPath:(NSString *)path;

//判断文件或文件夹是否存在, 是否为文件夹
- (BOOL)fileExistsAtPath:(NSString *)path isDirectory:(nullable BOOL *)isDirectory;
//eg:
NSFileManager *manage = [NSFileManager defaultManager];
BOOL dir = NO;//判断时，可以通过dir的地址，去更改dir的值
BOOL exist = [manage fileExistsAtPath:@"/Users/yan/Desktop/2.0.png" isDirectory:&dir];

//path 路径下的文件夹是否可读
- (BOOL)isReadableFileAtPath:(NSString *)path;

//path 路径下的文件夹是否可写
- (BOOL)isWritableFileAtPath:(NSString *)path;

//path 路径下的文件夹是否可删除
- (BOOL)isDeletableFileAtPath:(NSString *)path;

//path 路径下的文件夹是否可执行(不常用)
- (BOOL)isExecutableFileAtPath:(NSString *)path;
```
