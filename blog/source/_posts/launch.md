---
title: Launch
date: 2016-07-07 11:38:06
tags: Launch
categories : "UI"
---

###1.应用图标
    Launch Image Source
###2.启动图片
    Launch Screen
###3.修改状态栏的样式

    - (UIStatusBarStyle)preferredStatusBarStyle

###4.隐藏状态栏
    - (BOOL)prefersStatusBarHidden
###5.使用 KVC 的方式赋值
    [self setValuesForKeysWithDictionary:dict];
###6.让数组中的对象都执行一个方法
- makeObjectsPerformSelector
```objc
     [_answerView.subviews  makeObjectsPerformSelector:@selector(removeFromSuperview)];
 ```
- makeObjectsPerformSelector: 让数组中的对象都执行这个 removeFromSuperview 方法

###7.block 遍历数组
- enumerateObjectsUsingBlock:
```objc
    [_optionView.subviews enumerateObjectsUsingBlock:^(__kindof UIView * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
 // obj 数组中对象 UIView *类型的对象, 根据实际更改
 // idx 数组的下标
 // *stop = YES, 立即跳出遍历
 }];
 ```
 ###8.用户交互功能
 - userInteractionEnabled --> NO 禁止用户交互, 如果父View 设置了, 子view 也将不接受用户交互

 ###9.前置view
 ```objc
    [self.view bringSubviewToFront:_imageButton];
 self.view 必须是 _imageButton 的父view
```
