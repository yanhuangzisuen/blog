---
title: 字符串搜索
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---
## 前后缀检查

```objc
//1.是否以 aString 开头
- (BOOL)hasPrefix:(NSString *)aString;

//2.是否以 aString 结尾
- (BOOL)hasSuffix:(NSString *)aString;
```

## 字符串查找

```objc
//用于检查字符串内容是否包含 aString
//如果包含, 返回 aString 的范围
//如果不包含, NSRange 的 location 为 NSNotFound, length为0
- (NSRange)rangeOfString:(NSString *)aString;
```

## NSRange

* 常见结构体, 定义:

``` objc
typedef struct _NSRange {
    NSUInteger location;
    NSUInteger length;
}
//NSUInteger 的定义:无符号的整型
typedef unsigned int NSUInteger;
NSUInteger location : 表示该范围的起始位置
NSUInteger length : 表示该范围内的长度
```

* NSRange创建的几种方式

* 方式1:
```objc
NSRange range;
range.location = 7;
range.length = 3;
```

* 方式2:
```objc
    NSRange range = {7, 3};
    // or
    NSRange range = {.locatin = 7, .length = 3};
```

* 方式3:使用 NSMake 函数 OC中的结构体一般都有对应的 NSMake 函数
```objc
NSRange range = NSMakeRange(7, 3);
```
