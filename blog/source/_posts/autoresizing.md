---
title: Autoresizing
date: 2016-07-07 11:38:06
tags: Autoresizing
categories : "UI"
---

##autoresizing
    外部的四根线: 保持与父 view 的距离不变
    内部的两根线: 保持宽度和高度随着父 view 的改变而改变
    局限: 只能设置子 view 和父 view 之间的约束

#### 代码实现

```objc
UIViewAutoresizingNone                     外部四根线都都选
UIViewAutoresizingFlexibleLeftMargin       左侧灵活, 即右侧勾选
UIViewAutoresizingFlexibleWidth            宽度灵活, 即宽度勾选
UIViewAutoresizingFlexibleRightMargin      右侧灵活, 即左侧勾选
UIViewAutoresizingFlexibleTopMargin        上侧灵活, 即下侧勾选
UIViewAutoresizingFlexibleHeight           高度灵活, 即高度勾选
UIViewAutoresizingFlexibleBottomMargin     下侧灵活, 即上侧勾选

//eg:
blueView.autoresizingMask = UIViewAutoresizingFlexibleTopMargin | UIViewAutoresizingFlexibleLeftMargin;
```

###autolayout
- 约束
- 参照
- 核心公式: 宽度
 - 被约束 view 的宽度 = 参照 view 的宽度 * 系数 + 常量 constant

###NSLayoutConstraint
- VFL
 - 可视化格式语言
- Masonry
 - 第三方框架
 - 两个宏定义, 要放在导入头文件之前
 - mas_
 - 自动装箱

###sizeClass
- 把屏幕划分为九种
- any          任意       *
- compact   紧凑型  -
- regular     宽松型  +
- installed 属性 : 在不同类型的屏幕上面可以添加或取消控件
