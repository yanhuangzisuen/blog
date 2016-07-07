---
title: UIImageView
date: 2016-07-07 11:38:06
tags: UIImageView
categories : "UI"
---

###UIImageView 帧动画

	1. 可以展示单张图片
    2. 也可以用来播放动画
    3. 播放动画的方法
     - (void)startAnimating;//开始播放
     - (void)stopAnimating;//结束播放
     - (BOOL)isAnimating;//是否正在播放
    4. 用来存放动画图片的属性
     @property(nonatomic, copy) NSArray *animationImages;
    5. 播放的属性
     @property (nonatomic) NSTimeInterval animationDuration;//持续时间

     //如果不设置默认会无限循环播放
     @property (nonatomic) NSInteger      animationRepeatCount;//重复次数

```objc
//eg:
if ([self.imageView isAnimating]) return;

//动画数组
self.imageView.animationImages = arrM;

//设置播放动画的属性 ---- 必须在播放之前
self.imageView.animationDuration = 3;//时间
self.imageView.animationRepeatCount = 1;//次数

//开始动画
[self.imageView startAnimating];

//动画结束, 释放图片内存

dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(3.0 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    // 3.0s后自动执行这个block里面的代码
    self.imageView.animationImages = nil;
});

```

###读取图片的两种方式:

	imageNamed: 自动对图片做缓存
		优点: 第一次加载之后,  后面再使用直接读取缓存
		缺点: 会导致内存飙升
	imageWithContentOfFile: 不会做缓存  路径: NSBundle
		优点:  不做缓存
		缺点: 加载比较慢

### 拉伸图片

```objc
//方式一:
UIImage *resizeImage = [image resizableImageWithCapInsets:UIEdgeInsetsMake(halfHeight, halfWidth, halfHeight, halfWidth) resizingMode:UIImageResizingModeStretch];
//方式二:
Assets : Show Slicing
```

### Xcode 的 UUID
9AFF134A-08DC-4096-8CEE-62A4BB123046
插件的安装路径
~/Library/Application Support/Developer/Shared/Xcode/Plug-ins
