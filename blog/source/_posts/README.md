---
title: UI简介
date: 2016-07-07 11:38:06
tags: UI
categories : "UI"
---

`导航控制器的push的控制器的右滑弹出功能, 清空代理, 让导航控制器将功能找回`
`self.interactivePopGestureRecognizer.delegate = nil;`

## stroryboard 的认识
- 用于描述软件界面
- 默认情况下, 程序一启动就会加载 Main.storyboard
- 加载 storyboard 时, 会首先创建和显示箭头所指的控制器界面

## IBAction 和 IBOutlet
- IBAction
    - 本质就是 void
    - 能让方法具备连线的功能
- IBOutlet
    - 能让属性具备连线的功能

## storyboard 连线容易出现的问题
- 被连接的方法被删除, 但是连线没有去掉
    - 可能出现方法找不到的错误
    - unrecongnized selecotor sent to instance
- 连接的属性被删掉, 但是连线没有去掉
    - setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key

## UIViewController (控制器) 的认识
- 一个控制器负责管理一个界面
- 控制器负责界面的创建, 事件的处理等

## 类扩展
- 格式
-
```objc
@interface className()
/**
 *   属性, 方法的声明
 */
@end
```

- 作用
    - 为某个类添加额外的属性和方法的声明
    - 可以写在 .h 和 .m 文件中

## 项目属性
- Product Name
    - 软件名称、产品名称、项目名称
- Drganization Identifier
    - 公司的唯一标识
    - 一般是公司域名的反写, 比如 com.baidu
- Bundle Identifier
    - 软件的唯一标识
    - 一般是 Drganization Identifier + Product Name
