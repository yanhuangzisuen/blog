---
title: NSNumber
date: 2016-07-07 11:39:06
tags: NSNumber
categories : "Objective-C"
---

#### 1、【理解】NSNumber的介绍和使用

 * NSArray\NSDictionary中只能存放OC对象,不能存放int\float\double等基本数据类型。

 * 如果真想把基本数据(比如int)放进数组或字典中,需要先将基本数据类型包装成OC对象。
   * 基本数据类型（如int）--`包装`-->OC对象--`放进`-->数组/字典

 * NSNumber可以将基本数据类型包装成对象,这样就可以间接将基本数据类型存进NSArray\NSDictionary中
   * 基本数据类型（如int）--`包装`-->NSNumber对象--`放进`-->数组/字典

#### 2、【理解】NSNumber的创建
 * 以前

    ```objc
    + (NSNumber *)numberWithInt:(int)value;
    + (NSNumber *)numberWithDouble:(double)value;
    + (NSNumber *)numberWithBool:(BOOL)value;
    ```
 * 现在
```objc
@10;
@10.5;
@YES;
@(num);
```
#### 3、从NSNumber对象中得到基本类型数据

```objc
- (char)charValue;
- (int)intValue;
- (long)longValue;
- (double)doubleValue;
- (BOOL)boolValue;
- (NSString *)stringValue;

- (NSComparisonResult)compare:(NSNumber *)otherNumber;
- (BOOL)isEqualToNumber:(NSNumber *)number;
```
