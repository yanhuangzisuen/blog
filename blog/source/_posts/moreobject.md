---
title: 多个对象的内存管理
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

* 单个对象的内存管理，看起来非常简单。
* 如果对多个对象进行内存管理，并且对象之间是有联系的，那么管理就会变得比较复杂。


* 其实，多个对象的内存管理思路，跟管理游戏房间类似：
* 如：劲舞团，LOL
```objc
    // 1、创建玩家对象
    Gamer *game = [[Gamer alloc] init];

    // 2、创建房间对象
    Room *room = [[Room alloc] init];

    // 3、让玩家进入房间
    game.room = room;

    // 4、释放房间对象
    [room release];

    // 5、输出玩家的房间
    NSLog(@"玩家的房间是：%@",game.room);
```
* 此时，会报野指针错误。

### 多个对象内存管理原则

```objc
// 声明类
@interface Gamer : NSObject
{
    Room *_room;
}
- (void)setRoom:(Room *)room;
- (Room *)room;

// 实现类
@implementation Gamer
- (void)setRoom:(Room *)room
{

    [room retain];
    _room = room;
}
- (Room *)room{
    return _room;
}
- (void)dealloc
{
    NSLog(@"玩家被释放");
    [super dealloc];
}
@end

// main函数实现
  // 1、创建玩家对象
    Gamer *game = [[Gamer alloc] init];

    // 2、创建房间对象
    Room *room = [[Room alloc] init];

    // 3、让玩家进入房间
    game.room = room;

    // 4、释放房间对象
    [room release];

    // 5、输出玩家的房间
    NSLog(@"玩家的房间是：%@",game.room);

```
* 问题：房间无法被释放了怎么办？

* 解决方法：
 * 在对象被释放时，要把该对象的所有对象类型的成员变量在dealloc当中进行释放:

```objc
@implementation Gamer
- (void)dealloc
{
    [_room release];
    NSLog(@"玩家被释放");
    [super dealloc];
}
@end
```

* 需求：让玩家反复进入这个房间。

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Gamer *g = [Gamer new];

        Room *r = [Room new];

        g.room = r;
        g.room = r;
        g.room = r;

        [g release];
        [r release];

    }
    return 0;
}

```
* 问题：房间对象无法被释放，怎么办？

* 解决方案：判断新进房间与之前是否是同一个房间。

```objc
- (void)setRoom:(Room *)room
{
    if (_room != room) {
        [room retain];
        _room = room;

    }
}

```

* 总的来说，有以下几点规律：
 * 1）只要还有人使用某对象，那么这个对象就不会被回收。
 * 2）只要想要使用1个对象，那么就让对象的引用计数器+1。
 * 3）当不再使用这个对象时，就让对象的引用计数器-1。
