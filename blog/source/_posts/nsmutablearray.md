---
title: NSMutableArray
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

    1. NSMutableArray 是 NSArray 的子类, NSArray 是不可变的, 一旦初始化完毕后, 它里面的内容就永远固定的, 不能删除里面的内容, 也不能再往里面添加元素
    2. NSMutableArray 是可变的, 可以进行增\删\改操作


* NSMutableArray 添加元素

```objc
//添加一个元素
- (void)addObject:(id)object;

//添加 otherArray 的全部元素到当前数组中
- (void)addObjectsFromArray:(NSArray)array;

//在 index 位置插入一个元素 anObject
- (void)insertObject:(id)anObject atIndex:(NSUInteger)index;
```

* NSMutableArray 删除元素

```objc
//删除最后一个元素
- (void)removeLastObject;

//删除所有元素
- (void)removeAllObjects;

//删除 index 位置的元素
- (void)removeObjectAtIndex:(NSUInteger)index;

//删除特定的元素
- (void)removeObject:(id)object;

//删除 range 范围内的所有元素
- (void)removeObjectsInRange:(NSRange)range;
```

* NSMutableArray 替换元素

```objc
//用 anObject 替换 index 位置对应的元素
- (void)replaceObjectAtIndex:(NSUInteger)index withObject:(id)anObject;

//交换 idx1 和 idx2 位置的元素
- (void)exchangeObjectAtIndex:(NSUIntrger)idx1 withObjectAtIndex:(NSUInteger)idx2;
```

* NSMutableArray 简写

```objc
//设置元素
//之前
[array replaceObjectAtIndex:0 withObject:@"Jack"];

//现在
array[0] = @"Jack";
```

