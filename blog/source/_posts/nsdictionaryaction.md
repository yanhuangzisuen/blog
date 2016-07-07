---
title: NSDictionary常见用法
date: 2016-07-07 11:39:06
tags: NSDictionary
categories : "Objective-C"
---

* 返回字典的键值对数目

```objc
- (NSUInteger)count;
```

* 根据 key 取出对应的 value

```objc
- (id)objectForKey:(id)aKey;
```

* NSDictionary 的遍历

```objc
//快速遍历
for (NSString *key in dict) {
    //遍历 key
}

//block 遍历
[dict enumerateKeysAndObjectsUsingBlock:^(id key, id obj, BOOL *stop) {
    //遍历出 key 和 value
}];
```

