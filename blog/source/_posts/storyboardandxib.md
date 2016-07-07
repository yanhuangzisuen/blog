---
title: StoryboardAndXib
date: 2016-07-07 11:38:06
tags: StoryboardAndXib
categories : "UI"
---

### xib 和 storyboard 的异同点

    共同点: 可以设置 UI 界面

    不同的: storyboard(描述整个界面) 可以进行界面跳转, 是重量级的
            xib(描述局部界面) 轻量级


* xib

```objc
//返回一个数组 按 xib 拖放顺序
[[NSBundle mainBundle] loadNidNamed:@"xib的文件名" ower:nil options: nil];

loadNibNamed:  xib 的名字 返回数组
使用 loadNibNamed: 的原因
在项目文件中, xib 文件是以 .xib 结尾
安装之后, 就自动的以 .nib 结尾
执行command+R 相当于在模拟器上安装了应用程序

```

* storyboard

```objc
UIStoryboard *sb = [UIStoryboard storyboardWithName:@"ZXXLoteryHallViewController" bundle:nil];

//当前 storyboard 箭头所指的控制器
UIViewController = sb.instantiateInitialViewController;
```

