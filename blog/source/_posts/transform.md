---
title: Transform
date: 2016-07-07 11:38:06
tags: Transform
categories : "UI"
---

* 下面的方法是直接创建一个固定的 transform

```objc
//参数最多, 可定制性最强, 用的不多
CGAffineTransformMake(<#CGFloat a#>, <#CGFloat b#>, <#CGFloat c#>, <#CGFloat d#>, <#CGFloat tx#>, <#CGFloat ty#>);

//平移, 修改位置
CGAffineTransformMakeTranslation(<#CGFloat tx#>, <#CGFloat ty#>);

//缩放
CGAffineTransformMakeScale(<#CGFloat sx#>, <#CGFloat sy#>);

//旋转, 弧度 CGFloat == double
    M_PI == 一个π  M_PI_2 == π/2   M_1_PI = 1/π
CGAffineTransformMakeRotation(<#CGFloat angle#>);
```

* 每次累加当前的 transform, 连续动画

```objc
//持续旋转
CGAffineTransformRotate(<#CGAffineTransform t#>, <#CGFloat angle#>)

//持续缩放
CGAffineTransformScale(<#CGAffineTransform t#>, <#CGFloat sx#>, <#CGFloat sy#>)

//连续移动
CGAffineTransformTranslate(<#CGAffineTransform t#>, <#CGFloat tx#>, <#CGFloat ty#>)
```
