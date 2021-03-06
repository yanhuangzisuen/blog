---
title: set方法的内存管理
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

* 需求：
 * 1、让玩家换房间，进入1号房间后，再进入2号房间

```objc
// 实现玩家类
 @implementation Gamer
- (void)setRoom:(Room *)room
{
    [_room release];
    _room = [room retain];
}
- (Room *)room{
    return _room;
}
- (void)dealloc
{
    [_room dealloc];
    NSLog(@"玩家被释放");
    [super dealloc];
}
@end

int main(){
    // 1、创建玩家对象
    Gamer *game = [[Gamer alloc] init];

    // 2、创建房间对象
    Room *room = [[Room alloc] init];
    room.no = 1;

    Room *room1 = [[room alloc] init];
    room.no = 2;

    // 3、让玩家进入房间
    game.room = room;
    game.room = room1;

    // 4、释放房间对象
    [room release];

    // 5、释放玩家对象
    [game release];

    return 0;
}
```
* 问题：房间对象再次无法被释放
* 解决方案：

```objc
- (void)setRoom:(Room *)room
{
    if (_room != room) {
        // 释放旧房间
        [_room release];
        [room retain];
        _room = room;
    }
}
```

* 总结：
* 1、set方法的内存管理

```objc
- (void)setRoom:(Room *)room
{
    if (_room != room) {
    [_room release];
    _room = [room retain];
  }
}
```
* 2、dealloc方法内存管理

```objc
- (void)dealloc
{
    // 当玩家不在了，代表不用房间了
    // 对房间进行一次release
    [_room release];

    // 重写dealloc方法，必须在最后调用父类的dealloc方法
    [super dealloc];
}
```
* 常见错误写法
* 会引发内存泄露
 ```objc
gamer.room = [[Room alloc] init];
[[Room alloc] init].no= 10;
```
