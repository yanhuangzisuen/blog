---
title: NSDate
date: 2016-07-07 11:39:06
tags: NSDate
categories : "Objective-C"
---

#### 1、【理解】NSDate的介绍和使用

 *  NSDate可以用来表示时间,可以进行一些常见的日期\时间处理。
 * 一个NSDate对象就代表一个时间

#### 2、格式化日期

 ```objc
 NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
 formatter.dateFormat = @"yyyy-MM-dd HH:mm:ss";

 // 将NSString转换为NSDate
 NSDate *date = [formatter dateFromString:@"2010-03-24 00:00:00"];

 // 将NSDate转换为NSString
 NSLog(@"%@", [formatter stringFromDate:date]);
```
#### 3、计算日期

 * [NSDate date]返回的就是当前时间

#### 4、日期时间对象

 * 结合NSCalendar和NSDate能做更多的日期\时间处理
 * 获得NSCalendar对象

    ```objc
    NSCalendar *calendar = [NSCalendar currentCalendar];
    ```



 * 获得年月日

    ```objc
    - (NSDateComponents *)components:(NSCalendarUnit)unitFlags fromDate:(NSDate *)date;
    ```

 * 比较两个日期的差距

    ```objc
    - (NSDateComponents *)components:(NSCalendarUnit)unitFlags fromDate:(NSDate *)startingDate toDate:(NSDate *)resultDate options:(NSCalendarOptions)opts;
    ```
