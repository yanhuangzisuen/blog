---
title: UICollectionView
date: 2016-07-07 11:38:06
tags: UICollectionView
categories : "UI"
---

###UICollectionView
####1. 实例化 collectionView 必须传入一个非空的 layout 布局对象
- UICollectionViewLayout
- UICollectionViewFlowLayout 是 UICollectionViewLayout 的子类

####2. 注册 cell

- class
- xib  必须设置重用标识符 registerNib
- storyboard prototype  必须设置重用标识符

####3. flowLayout

- itemSize 设置 cell 的大小
- sectionInsets 设置组的内边距
- scrollDirection 设置滚动方向
- minimumInterItemSpacing 列间距(垂直方向)
- minimumLineSpacing  行间距(垂直方向)

####4.组头/组尾

- 必须通过代理方法进行重用返回
- 如果通过 storyboard 拖拽显示, 必须设置重用标识符, 不然代理方法不会执行

####悬浮效果
```objc
- flowLayout.sectionHeaderPinToVisibleBounds = YES;
- flowLayout.sectionFooterPinToVisibleBounds = YES;
```
####设置组头/组尾的 size, 也与滚动方向有关

```objc
flowLayout.headerReferenceSize = CGSizeMake(垂直滚动时无效, 水平滚动时无效);
flowLayout.footerReferenceSize = CGSizeMake(垂直滚动时无效, 水平滚动时无效);
```

