---
title: NSMutableDictionary
date: 2016-07-07 11:39:06
tags: NSDictionary
categories : "Objective-C"
---

    1. NSMutableDictionary 是 NSDictionary 的子类, NSDictionary 是不可变的, 一旦初始化完毕后, 它里面的内容就永远固定的, 不能删除里面的内容, 也不能再往里面添加元素
    2. NSMutableDictionary 是可变的, 可以进行增\删\改操作

## NSMutableDictionary 的常见用法

* 添加\修改操作

```objc
//添加一个键值对(如果字典中存在这个 key, 会将之前对应的值替换掉)
- (void)setObject:(id)anObject forKey:(id<NSCopying>)aKey;
```

* 删除操作

```objc
//通过 aKey 删除对应的 value
- (void)removeObjectForKey:(id)aKey;

//删除所有的键值对
- (void)removeAllObjects;
```

## NSMutableDictionary 的简写

* 设置键值对

```objc
//before
[dict setObject:@"Jack" forKey:@"name"];

//now
dict[@"name"] = @"Jack"
```
