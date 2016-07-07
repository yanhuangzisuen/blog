---
title: 字符串的截取和替换
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---
## 字符串的截取

```objc
//1.从指定位置from(包含指定位置的字符)开始到结尾
- (NSString *)substringFromIndex:(NSUInteger)from;

//2.从字符串的开头一直截取到指定的位置to(不包含该位置的字符)
- (NSString *)substringToIndex:(NSUInteger)to;

//3.按照所给的NSRange从字符串中截取子串
- (NSString *)substringWithRange:(NSRange)range;
```

## 字符串的替换

```objc
//用 replacement 替换 target
- (NSString *)stringByReplacingOccurrencesOfString:(NSString *)target withString:(NSString *)replacement;
```

## 字符串与路径

```objc
//是否是绝对路径
- (BOOL)isAbsolutePath;

//获得最后一个目录
- (NSString *)lastPathComponent;

//删除最后一个目录
- (NSString *)stringByDeletingLastPathComponent;

//在路径的后面拼接一个目录
- (NSString *)stringByAppendingPathComponent:(NSString *)str;
//or 使用stringByAppendingString:或者stringByAppendingFormat:拼接字符串内容
```

## 字符串与文件扩展名

```objc
//获取扩展名
- (NSString *)pathExtension;

//删除尾部扩展名
- (NSString *)stringByDeletingPathExtension;

//在尾部添加扩展名
- (NSString *)stringByAppendingPathExtension:(NSString *)str;
```
