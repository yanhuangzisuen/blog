---
title: 字符串的比较
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---

## NSString的大小写处理

```objc
//全部转大写
- (NSString *)uppercaseString;
//全部转小写
- (NSString *)lowercaseString;
//首字母大写, 其它变小写
- (NSString *)capitalizedString;
```

## 字符串的比较

* 1.两个字符串的内容相同就返回YES, 否则返回NO

```objc
- (BOOL)isEqualToString:(NSString *)aString;
```

* 2.比较两个字符串内容的大小

```objc
//比较方法:逐个字符进行比较ASCII值, 只要有有一个值能够比较出大小, 就返回NSComparisonResult作为比较结果
/**
NSComparisonResult是一个枚举，有3个值:
如果左侧  <  右侧,返回NSOrderedAscending,-1L
如果左侧  >  右侧,返回NSOrderedDescending,
如果左侧  == 右侧,返回NSOrderedSame
*/

//区分大小写比较
- (NSComparisonResult)compare:(NSString *)string;
//忽略大小写比较
- (NSComparisonResult) caseInsensitiveCompare:(NSString *)string;
```
* eg:

```objc
NSString *str = @"adc";
NSString *str2 = @"ADc";
NSComparisonResult result = [str compare:str2];
switch (result) {
  case NSOrderedDescending:
       NSLog(@"str > str2");
       break;
  case NSOrderedAscending:
       NSLog(@"str < str2");
       break;
  case NSOrderedSame:
       NSLog(@"str == str2");
       break;
}
```
* eg:

```objc
 NSString *str = @"aBc";
 NSString *str1 = @"abc";

 // 忽略大小写字符串比较
 NSComparisonResult result = [str caseInsensitiveCompare:str1];

// 因为忽略B和b,所以str = str1
  NSLog(@"%ld",result);
```
