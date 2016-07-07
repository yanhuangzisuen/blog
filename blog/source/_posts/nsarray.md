---
title: NSArray
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

## 常见的创建方法

```objc
+ (instancetype)array;
+ (instancetype)arrayWithObject:(ObjectType)anObject;
+ (instancetype)arrayWithObjects:(ObjectType)firstObj, ... ;
+ (instancetype)arrayWithArray:(NSArray<ObjectType> *)array;
+ (id)arrayWithContentsOfFile:(NSString *)path;
+ (id)arrayWithContentsOfURL:(NSURL *)url;

//将 NSArray 保存到文件中
- (BOOL)writeToFile:(NSString *)path  atomically:(BOOL)useAuxiliaryFile;
- (BOOL)writeToURL:(NSURL *)url atomically:(BOOL)atomically;
```

## 注意事项:
* 只能存放任意对象, 并且是有序的
* 不能存放非OC对象, 比如int\float\double\char\enum\struct等
* 它是不可变, 一旦初始化完毕后, 它里面的内容就永远是固定的, 不能删除里面的元素, 也不能再往里面添加元素
