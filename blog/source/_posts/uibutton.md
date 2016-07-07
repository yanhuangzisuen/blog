---
title: UIButton
date: 2016-07-07 11:38:06
tags: UIButton
categories : "UI"
---

* 解决按钮按下不立即变色问题

```objc
//自定义 button, 重写该方法
- (void)setHighlighted:(BOOL)highlighted
{
    //如果调用父类的 setHighlighted, 那么点击下去, 不会立即变色
//    [super setHighlighted:highlighted];
}
```

* button有多种状态, 它提供了一些便捷属性，可以直接获取当前状态下的文字、文字颜色、图片等

```objc
 @property(nonatomic,readonly,retain) NSString *currentTitle;
 @property(nonatomic,readonly,retain) UIColor  *currentTitleColor;
 @property(nonatomic,readonly,retain) UIImage  *currentImage;
 @property(nonatomic,readonly,retain) UIImage  *currentBackgroundImage;
```
* 设置button 的水平对齐方式

```objc
UIControlContentHorizontalAlignmentCenter = 0,
UIControlContentHorizontalAlignmentLeft   = 1,
UIControlContentHorizontalAlignmentRight  = 2,
UIControlContentHorizontalAlignmentFill   = 3,
```

```objc
//button.contentMode --> 设置image
//UIControl内容的排布方式 contentHorizontalAlignment -- contentVerticalAlignment
```

