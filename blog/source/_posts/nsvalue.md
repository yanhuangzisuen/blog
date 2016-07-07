---
title: NSValue
date: 2016-07-07 11:39:06
tags: NSValue
categories : "Objective-C"
---

#### 1、NSNumber是NSValue的子类, 但NSNumber只能包装数字类型
#### 2、NSValue可以包装任意值，因此,可以用NSValue将结构体包装后, 加入NSArray\NSDictionary中。

#### 3、常见结构体包装
 * 为了方便 结构体 和NSValue的转换,Foundation提供了以下方法：
 * 将结构体包装成NSValue对象

```objc
+ (NSValue *)valueWithPoint:(NSPoint)point;
+ (NSValue *)valueWithSize:(NSSize)size;
+ (NSValue *)valueWithRect:(NSRect)rect;
```
 * 从NSValue对象取出之前包装的结构体

```objc
- (NSPoint)pointValue;
- (NSSize)sizeValue;
- (NSRect)rectValue;
```

#### 4、任意数据的包装

* NSValue提供了下列方法来包装任意数据

```objc
+ (NSValue *)valueWithBytes:(const void *)value objCType:(const char *)type;
//value参数 : 所包装数据的地址
//type 参数 : 用来描述这个数据类型的字符串,用@encode指令来生成。
```

* 从NSValue中取出所包装的数据

```objc
- (void)getValue:(void *)value;
```

* eg:

```objc
//    包装自定义结构体
    typedef struct{
        char *name;
        int age;
        double height;
    } Perosn;
    Perosn p = {"zhangsan", 18, 175.2};
//    2.1.valueWithBytes 接收一个指针,需要传递 需要包装的结构体变量的地址
//    2.2.objCType 需要传递需要包装的数据类型 需要  @encode 生成
    NSValue *pValue = [NSValue valueWithBytes:&p objCType:@encode(Perosn)];
    NSArray *arr = @[pValue];
    NSLog(@"%@", arr);
//    2.3从NSArray中取出保存的结构体变量
    Perosn res;
    [pValue getValue:&res];
    NSLog(@"name = %s, age = %i, height = %.2f", res.name, res.age, res.height);
```
