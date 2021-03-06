---
title: MRC
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

#### 1、关闭ARC的方法

* 1.设置项目信息
![](/img/3.1.png)

#### 2、手动管理（MRC）快速入门

* 内存管理的关键：如何判断对象被回收？

* 重写dealloc方法,代码规范
 * 一定要[super dealloc],而且要放到最后,意义是:你所创建的每个类都是从父类, 基类继承来的,有很多实例变量也会继承过来,这部分变量有时候会在你的程序内使用,它们不会自动释放内存,你需要调用父类的dealloc方法来释放,然而在此之前你需要先把自己所写类中的变量内存先释放掉,否则就会造成你本类中的内存积压,造成泄漏。

* 注意
 * 永远不要直接通过对象调用dealloc方法(实际上调用并不会出错)
 * 一旦对象被回收了,它占用的内存就不再可用,坚持使用会导致程序崩溃(野指针错误)为了防止调用出错,可以将“野指针”指向nil(0)。
```objc
   // 1.创建学生
    Student *s = [[Student alloc] init];

    // 2.查看学生引用计数器
    NSUInteger count = [s retainCount];

    // 3、输出学生的引用计数器值
    NSLog(@"%lu",count);
    ```
* 重写dealloc

  ```objc
   #import "Student.h"

   @implementation Student
   - (void)dealloc
   {
     NSLog(@"对象即将被释放---");
     [super dealloc];
   }
  ```
* dealloc是NSObject提供的对象方法，只能由系统自动调用。
* 当对象的引用计数器值为 0 时，系统会自动调用dealloc方法。

* 总结：程序人员可以通过操纵引用计数器的值来控制对象是否被回收。这是MRC内存管理的核心内容。
