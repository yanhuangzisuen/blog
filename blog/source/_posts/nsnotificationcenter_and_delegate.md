---
title: NSNotificationCenter And Delegate
date: 2016-07-07 11:38:06
tags: NSNotificationCenter And Delegate
categories : "UI"
---

### 代理
* 代理设计模式的作用:
    * 1.A对象监听B对象的一些行为，A成为B的代理
    * 2.B对象想告诉A对象一些事情，A成为B的代理

* 代理设计模式的总结：
    * 如果你想监听别人的一些行为，那么你就要成为别人的代理
    * 如果你想告诉别人一些事情，那么就让别人成为你的代理

* 代理设计模式的开发步骤
    * 1.拟一份协议（协议名字的格式：控件名 + Delegate），在协议里面声明一些代理方法（一般代理方法都是@optional）
    * 2.声明一个代理属性：@property (nonatomic, weak) id<代理协议> delegate;
    * 3.在内部发生某些行为时，调用代理对应的代理方法，通知代理内部发生什么事
    * 4.设置代理：xxx.delegate = yyy;
    * 5.yyy对象遵守协议，实现代理方法

### 代理和通知的区别
- 代理：1个对象只能告诉另1个对象发生了什么事
- 通知：1个对象可以告诉N个对象发生了什么事

### KVC\KVO
- KVC(Key Value Coding)常见作用：给模型属性赋值
- KVO(Key Value Observing)常用作用：监听模型属性值的改变
- KVO的使用步骤<br>

```objc
// cc监听了aa的name属性的改变
[aa addObserver:cc forKeyPath:@"name" options: NSKeyValueObservingOptionOld context:nil];

// cc得实现监听方法
/**
 * 当监听到object的keyPath属性发生了改变
 */
- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context
{
    NSLog(@"监听到%@对象的%@属性发生了改变， %@", object, keyPath, change);
}
```

###通知
```objc
//到通知中心添加监听者
[[NSNotificationCenter defaultCenter] addObserver:<#(non null id)#> selector:<#(non null SEL)#> name:<#(nullable NSString *)#> object:<#(nullable id)#>]
//发布通知
[[NSNotificationCenter defaultCenter] postNotificationName:<#(non null NSString *)#> object:<#(nullable id)#> userInfo:<#(nullable NSDictionary *)#>]
//监听者对象被销毁的时候, 把监听者从通知中心移除
[[NSNotificationCenter defaultCenter] removeObserver:<#(non null id)#>]
```
###代理和通知
- 共同点
 - 发送消息
- 不同点
 - 代理: 一对一
 - 通知:多对多

###日期转换
```objc
//获取当前时间
NSDate *nowDate = [NSDate date];
//设置时间的格式
NSDateFormatter *formatter = [[NSDateFormatter alloc] init]
formatter.dateFormat = @“yyyy-MM-dd HH:mm:ss”;
//NSDate 转 NSString
NSString *str = [formatter stringFromDate:nowDate];
```
