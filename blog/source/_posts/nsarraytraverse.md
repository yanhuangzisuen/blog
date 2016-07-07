---
title: NSArray的遍历
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

**遍历, 就是将 NSArray 里面的所有元素一个一个取出来查看**

* 普通 for 循环

```objc
for (NSUInteger i = 0; i < array.count; i++) {
    //对应 i 下标的元素
    id = array[i];
}
```

* 增强 for 循环

```objc
for (id obj in array) {
    //obj 数组中的元素
}
```

* block进行遍历(迭代器)

```objc
[array enumerateObjectsUsingBlock:^(id obj, NSUInteger idx, BOOL *stop) {
    //obj 对应下标 idx 的数组中的元素
    // stop 控制循环的终止
}];
```
