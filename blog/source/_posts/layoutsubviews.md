---
title: LayoutSubViews
date: 2016-07-07 11:38:06
tags: LayoutSubViews
categories : "UI"
---

## layoutSubviews总结
- 1.iOS layout机制相关方法
 ```objc
 - (CGSize)sizeThatFits:(CGSize)size
 - (void)sizeToFit
 ```
 ```objc
 - (void)layoutSubviews
 - (void)layoutIfNeeded
 - (void)setNeedsLayout
 ```
 ```objc
 - (void)setNeedsDisplay
 - (void)drawRect
 ```
- 2.layoutSubviews 被调用的情况

```objc
 1.init 初始化时不会触发 layoutSubview, 但是使用 initWithFrame: 进行初始化时, 当 rect 的值不为 CGRectZero 时, 会触发
 2.addSubview 会触发 layoutSubviews
 3.设置 view 的Frame 会触发 layoutSubviews, 前提是 Fraame的值前后发生变化
 4.滚动一个 UIScrollView 会触发 layoutSubviews
 5.旋转 Screen 会触发 父View 上的 layoutSubviews 事件
 6.改变一个 UIView 大小的时候, 也会触发 父View 上的 layoutSubviews 事件
 在苹果的官方文档中强调:
    You should override this method only if the autoresizing and constraint-based behaviors of the subviews do not offer the behavior you want.
    只要调整尺寸和基于约束的行为的子视图不提供你想要的行为时, 你应重写此方法
```
- 3.刷新子对象布局

```objc
- layoutSubviews: 这个方法默认没有做任何事情, 需要子类进行重写
- setNeedsLayout: 标记为需要重新布局, 异步调用 layoutIfNeeded 刷新布局, 不立即刷新, 但 layoutSubviews 一定会调用
- layoutIfNeeded: 如果有需要刷新的标记, 立即调用 layoutSubviews 进行布局, 如果没有标记, 不会调用 layoutSubviews
对于 layoutSubviews 文档中还指出:
    You should not call this method directly. If you want to force a layout update, call the setNeedsLayout method instead to do so prior to the next drawing update. If you want to update the layout of your views immediately, call the layoutIfNeeded method
    你不应该直接调用该方法, 如果你想更新布局, 在更新布局之前调用 [view setNeedsLayout] 方法. 如果你想立即更新你的视图, 则调用 [view layoutIfNeeded] 方法.
在视图第一次显示之前, 标记总是 "需要刷新" 的, 可以直接调用 [view layoutIfNeeded]
```
- 4.重绘

```objc
- drawRect:(CGRect)rect: 重写此方法, 执行重绘任务
- setNeedsDisplay: 标记为需要重绘, 异步调用 drawRect: 方法
- setNeedsDisolayInRect:(CGRect)invalidRect: 标记需要局部重绘
```
- 5.sizeToFit 与 sizeThatFits:

```objc
- (void)sizeToFit
sizeToFit 可以被手动直接调用
调用 sizeToFit 会自动调用 sizeThatFits: 方法
sizeToFit 不应该在子类中被重写, 应该重写 - (CGSize)sizeThatFits:(CGSize)size
/**
 *  调整尺寸
 *
 *  @param size receiver当前的尺寸
 *
 *  @return 返回一个合适的尺寸
 */
- (CGSize)sizeThatFits:(CGSize)size
```
- 6.layoutSubviews 与 drawRect

```objc
layoutSubviews 对 subviews 重新布局

layoutSubviews 方法调用先于 drawRect

setNeedsLayout 在receiver标上一个需要被重新布局的标记，在系统 runloop 的下一个周期自动调用 layoutSubviews

layoutIfNeeded 方法如其名，UIKit 会判断该receiver是否需要 layout.根据Apple官方文档, layoutIfNeeded 方法应该是这样的

layoutIfNeeded 遍历的不是 superview 链，应该是 subviews 链

drawRect 是对receiver的重绘，能获得 context

setNeedDisplay 在receiver标上一个需要被重新绘图的标记，在下一个draw周期自动重绘，iphone device的刷新频率是60hz，也就是1/60秒后重绘
```
