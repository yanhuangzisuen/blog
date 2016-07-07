---
title: NSMutableString
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---

**NSMutableString 是可变字符串, 是NSString 的子类.**

1. NSString 是不可变的, 里面的文字内容是不能进行修改的.
2. NSMutableString 是可变的, 里面的文字内容可以随时改变.
3. `NSMutableString 能使用 NSString 的所有方法`

## 常见用法

```objc
//拼接 aString 到最后面
- (void)appendString:(NSString *)aString;

//拼接一段格式化字符串到最后面
- (void)appendFormat:(NSString *)format, ...;

//删除 range 范围内的字符串
- (void)deleteCharactersInRange:(NSRange)range;

//在 loc 这个位置插入 aString
- (void)insertString:(NSString *)aString atIndex:(NSUInteger)loc;

//使用aString替换range范围内的字符串
- (void)replaceCharactersInRange:(NSRange)range withString:(NSString *)aString;
```
