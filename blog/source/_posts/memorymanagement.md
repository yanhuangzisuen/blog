---
title: 内存管理
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

#### 1、为什么要进行内存管理？

* 在程序开发中，应该及时将不用的数据回收，合理分配和管理内存 ，以提高程序的运行效率。
* 哪些行为会增加内存占用？
 * 创建1个OC对象
 * 定义1个变量
 * 调用1个函数或者方法

####2、OC内存管理的范围

 * 管理范围：
 * `管理任何继承NSObject的对象，对其他的基本数据类型无效。`
 * 本质原因：是因为对象和其他数据类型在系统中的存储空间不一样，其他局部变量主要存放于栈中，而对象存储于堆中。当代码块结束时，这个代码块中涉及的所有局部变量会被回收，指向对象的指针也被回收，此时，对象已经没有指针指向，但依然存在于内存中，造成内存泄露。
