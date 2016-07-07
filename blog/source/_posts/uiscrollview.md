---
title: UIScrollView
date: 2016-07-07 11:38:06
tags: UIScrollView
categories : "UI"
---

##缩放
    设置最大能方法多少倍
    最小能缩小多少倍
    告诉 scrollView 要对哪个 view 进行缩放(代理方法)
##滚动
    contentSize —滚动范围
    contentInset — 内边距
    contentOffset — 偏移量(内容滚动到某个点)

##UIScrollView的常见属性

    //不要自动调整insets, 自己设置contentInset
    self.automaticallyAdjustsScrollViewInsets = NO;

    滚动范围: contentSize --> 要比 scrollView 的 size 大

    内边距 : contentInset --> (滚动到边界的时候) imageView 的边框距离 scrollView 边框的距离

    偏移量 : contentOffset --> 是滚动到某个位置(点)

    弹簧效果 : bounces --> 默认 YES, 一般不关闭

    分页效果(以 scrollView 的宽度进行分页) :
    _scrollView.pagingEnabled = YES;

    总有弹簧效果 : 就算不设置 contentSize 也可以有弹簧效果, 前提是 bounces = YES;
    alwaysBounceHorizontal
    alwaysBounceVertical

    滚动指示器 : 默认是 YES, 打开的
    showsHorizontalScrollIndicator
    showsVerticalScrollIndicator

    是否可以滚动 :
    scrollEnabled = YES;

## `无法滚动的原因`

1. `contentSize 小于 scrollView.size`
2. `scrollEnable = NO;`
3. `userInteractionEnabled = NO;禁止用户交互`


## pageControl 注意属性:
    1.numberOfPages --> 设置点数
    2.currentPage --> 当前位置 取值0 ~ numberOfPages - 1;
    3.currentPageIndicatorTintColor --> 当前指示器的颜色
    4.pageIndicatorTintColor --> 非当前指示器的颜色

## NSTimer 的使用
        scheduled : 计划
        Interval : 间隔
        target : 一般指控制器
        selector : 方法
        uesrInfo : 用户自定义的参数
        repeats : 重复

        一旦创建就会立即执行

        invalidate 无效后, 要再次使用, 需要重新创建timer
        fire 立即执行, 不会等待 Interval 设置的时间

```objc
 + (NSTimer *)scheduledTimerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(nullable id)userInfo repeats:(BOOL)yesOrNo;

 NSRunLoop *mainLoop = [NSRunLoop mainRunLoop];
    /*
     设置优先级
     NSDefaultRunLoopMode;
     NSRunLoopCommonModes//优先级更高, 拖拽时定时器不会停止
     */
[mainLoop addTimer:_timer forMode:NSRunLoopCommonModes];
```

## 使用 delegate :

1. 修饰符必须使用 weak, 防止循环引用
2. 如果两个对象相互引用, 其中一个必须是 weak
3. addSubview --> 强引用

## UIScrollViewDelegate

```objc
//滚动完毕就会调用（如果不是人为拖拽scrollView导致滚动完毕，才会调用这个方法
- (void)scrollViewDidEndScrollingAnimation:(UIScrollView *)scrollView
{
    
}
```

#### 拖拽

* 当 scrollView 内容滚动时, 就会调用

```objc
- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    NSLog(@"滚动时调用")
}
```

* deagg : 拖拽, 开始拖拽的时候调用

```objc
- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView {
     NSLog(@"开始拖拽");
}
```

* 停止拖拽是调用

```objc
- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate {
    NSLog(@"停止拖拽");
}
```

#### 缩放

* 返回的 view 将被拉伸/缩放

```objc
- (UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView {
    return _imageView;
}
```

* 只要图片在放大/缩小时一直调用

```objc
- (void)scrollViewDidZoom:(UIScrollView *)scrollView {
    NSLog(@"缩放时调用");
}
```

* 开始缩放的时候调用

```objc
//withView : 进行缩放的 view
- (void)scrollViewWillBeginZooming:(UIScrollView *)scrollView withView:(UIView *)view {
    NSLog(@"开始缩放的时候调用");
}
```

* 结束的时候调用

```objc
//withView : 进行缩放的 view
//atScale : 缩放的倍数
- (void)scrollViewDidEndZooming:(UIScrollView *)scrollView withView:(UIView *)view atScale:(CGFloat)scale {
    NSLog(@"结束的时候调用");
}
```
