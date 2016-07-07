---
title: ARC循环引用
date: 2016-07-07 11:39:06
tags: ARC
categories : "Objective-C"
---

* 1、ARC下循环引入问题
* 一个人拥有一只狗，一只狗拥有一个主人。
![](/img/311.png)

![](/img/312.png)
* 当增加d.owner = p;时形成循环引用。
![](/img/313.png)
#####解决方法：一端用strong，一端用weak。

* 2、ARC下@property参数

```objc
ARC中的@property
strong : 用于OC对象, 相当于MRC中的retain
weak : 用于OC对象, 相当于MRC中的assign
assign : 用于基本数据类型, 跟MRC中的assign一样
copy : 一般用于NSString, 跟MRC中的copy一样

在ARC情况下解决”循环retain”的问题:@property一边用strong,一边用weak。
```

### ARC特点总结
 * 1）不允许调用release,retain,retainCount
 * 2）允许重写dealloc,但是不允许调用[super dealloc]
 * 3）@property的参数:
   * strong:相当于原来的retain(适用于OC对象类型),成员变量是强指针
   * weak:相当于原来的assign,(适用于oc对象类型),成员变量是弱指针
   * assign:适用于非OC对象类型(基础类型)

### ARC使用注意事项

 * 1）ARC中,只要弱指针指向的对象不在了,就直接把弱指针做清空(赋值为nil)操作。

 * 2）__weak Person *p=[[Personalloc]init];//不合理
 * 对象一创建出来就被释放掉,对象释放掉后,ARC把指针设置为nil。

 * 3）ARC中在property处不再使用retain,而是使用strong,在dealloc中不需要再 [super dealloc]。
 * @property(nonatomic,strong)Dog *dog;
// 意味着生成的成员变量_dog是一个强指针,相当于以前的retain。

 * 4）如果换成是弱指针,则换成weak,不需要加_ _。


## ARC的兼容和转换

* 1、ARC模式下如何兼容非ARC的类
 * 让程序兼容ARC和非ARC部分。转变为非ARC -fno-objc-arc 转变为ARC的, -f-objc-arc 。
![](/img//1.png)
![](/img//11.png)
![](/img//12.png)

* 2、将MRC转换为ARC
 * ARC也需要考虑循环引用问题：一端用strong，一端用weak。
 * `提示：字符串是特殊的对象，但是不需要使用release手动释放，这种字符串对象默认就是autorelease，不需要额外管理内存。`
 * 如果一个项目是MRC的，那么我们可以把这个项目转换成ARC。
![](/img//13.png)
![](/img//2.png)
![](/img//3.png)
![](/img//4.png)
![](/img//5.png)
