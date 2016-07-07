---
title: UIView
date: 2016-07-07 11:38:06
tags: UIView
categories : "UI"
---

## UIView 的常见属性

- NSArray *subviews
    - 所有的子控件
    - 数组元素的顺序决定着子控件的显示层级顺序 (下标越大的, 越显示在上面)

## UIView 的常见方法

    1.tag  标识
    2.removeFromSuperview  想要删除哪个控件, 就调用那个控件的方法
    3.addSubView  添加子控件
    4.SubViewS 获取所有的子控件
    5.viewWithTag 通过 tag 获取子控件, 优先获取自己的 tag
    6.frame  决定了控件的位置和尺寸
    7.transform  可以改变位置, 大小, 旋转  一套创建固定值, 一套在原有基础上偏移

- addSubview:
    - 添加一个子控件
    - 使用这个方法添加的子控件会被塞到 subviews 数组的最后面
- 可以使用下面的方法调整子控件在 subview 数组中的顺序

```objc
//将子控件 view 插入到 subviews 数组的 index 位置
- (void)insertSubview:(UIView *)view atIndex:(NSInteger)index;

//将子控件 view 显示到子控件 siblingSubview 的下面
- (void)insertSubview:(UIView *)view belowSubview:(UIView *)siblingSubview;

//将子控件 view 显示到子控件 siblingSubview 的上面
- (void)insertSubview:(UIView *)view aboveSubview:(UIView *)siblingSubview;

//将子控件 view 放在数组的最后面, 显示在最上面
- (void)bringSubviewToFront:(UIView *)view;

//将子控件 view 放在数组的最前面, 显示在最下面
- (void)sendSubviewToBack:(UIView *)view;
```
## 代码创建控件 —UIView
	1.alloc init
	2.修改 frame
	3.设置颜色	backgroundColor
	4.添加到控制器的 View	addSubview
### viewDidLoad
	在控制器的 View 加载到内存中的时候, 就会运行
	一般在这里, 初始化数据, 或者创建控件等等
### 创建按钮
	1.创建某一种 type 的按钮	UIButton *bun = [UIButton buttonWithType:UIButtonTypeCustom];
	2.frame
	3.文字	 [bun setTitle:	forState:(UIControlState)];
	4.文字颜色	setTitleColor: forState:
	5.设置图片	setBackgroundImage: forState:
	6.设置背景图片	setImage: forState:
	7.绑定方法(事件)	addTarget:(nullable id) action:(non null SEL) forControlEvents:(UIControlEvents)
		addTarget : 添加哪个类的方法
		action : 绑定哪个方法	@selector()	生成
		forControlEvents : 触发方式
	8.添加	addSubview:


## 九宫格计算思路
- 利用控件的索引index计算出控件所在的行号和列号
- 利用列号计算控件的x值
- 利用行号计算控件的y值

## HUD
- 其他说法：指示器、遮盖、蒙板
- 半透明HUD的做法
    - 背景色设置为半透明颜色

## 定时任务
- 方法1：performSelector

```objc
// 1.5s后自动调用self的hideHUD方法
[self performSelector:@selector(hideHUD) withObject:nil afterDelay:1.5];
```
- 方法2：GCD

```objc
dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(1.5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    // 1.5s后自动执行这个block里面的代码
    self.hud.alpha = 0.0;
});
```
- 方法3：NSTimer

```objc
// 1.5s后自动调用self的hideHUD方法
[NSTimer scheduledTimerWithTimeInterval:1.5 target:self selector:@selector(hideHUD) userInfo:nil repeats:NO];
// repeats如果为YES，意味着每隔1.5s都会调用一次self的hidHUD方法
```

## 常见问题
- 项目里面的某个.m文件无法使用
    - 检查：Build Phases -> Compile Sources
- 项目里面的某个资源文件（比如plist、音频等）无法使用
    - 检查：Build Phases -> Copy Bundle Resources

###xib
	描述局部界面, 解决界面问题 代码与逻辑处理需要与类进行关联
	属于轻量级别,
	返回数组 [NSBundle mainBundle] loadNibNamed: owner: options:
	重写 setter 方法, 一定要先给属性赋值
###MVC 模式
	M —> Model	描述数据, 处理数据
	V —> View	展示界面
	C —> Controller	用户交互的逻辑处理, 管理 view 的生命周期

## 模型
- 什么是模型？
    - 专门用来存放数据的对象
    - 一般都是一些直接继承自NSObject的纯对象
    - 内部会提供一些属性来存放数据

## 一个控件看不见有哪些可能？
- 宽度或者高度其实为0
- 位置不对（比如是个负数或者超大的数，已经超出屏幕）
- hidden == YES
- alpha <= 0.01
- 没有设置背景色、没有设置内容
- 可能是文字颜色和背景色一样
- 检查父 View 的上面几种情况
