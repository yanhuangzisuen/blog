---
title: 手动管理内存的原则
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

#### 1、内存管理的原则
* 1.原则
 * 只要还有人在使用某个对象,那么这个对象就不会被回收;
 * 只要你想使用这个对象,那么就应该让这个对象的引用计数器+1;
 * 当你不想使用这个对象时,应该让对象的引用计数器-1;

* 2.谁创建,谁release
 * 1)如果你通过alloc,new,copy来创建了一个对象,那么你就必须调用release或者 autorelease方法.
 * 2)不是你创建的就不用你去负责

* 3.谁retain,谁release
 * 只要你调用了retain,无论这个对象时如何生成的,你都要调用release

* 4.总结
 * 有始有终,有加就应该有减。曾经让某个对象计数器加1,就应该让其在最后-1.

#### 2、内存管理研究内容

* 1.野指针(僵尸对象)
 * 僵尸对象: 已经被销毁的对象(不能再使用的对象).
 * 野指针:指向僵尸对象(不可用内存)的指针.
 * 空指针: 没有指向存储空间的指针(里面存的是nil, 也就是0)
* 2.内存泄露
 * 如果在程序结束后，对象没有被释放，此时称为内存泄露。

```
 Student *s = [[Student alloc] init];
 Student *s1 = [s retain];
 ```
* 那么，问题来了，最后由谁释放？
* 1> 由s释放
```
 Student *s = [[Student alloc] init];
 Student *s1 = [s retain];

 [s release];
 [s release];
 ```

* 2> 由s1释放

 ```objc
 Student *s = [[Student alloc] init];
 Student *s1 = [s retain];

 [s1 release];
 [s1 release];

 ```
 * 两种方式都可以释放内存。
 * 但是，如果没有一种统一的释放原则，那么就会造成代码的混乱，舍都可以释放, 好比一个公司所有的领导没有分工一样, 任何事儿, 任何一个领导都可以插一嘴，很显然这样就没法干了， 因此需要有一个规范去约束使用。

#### 单个对象的野指针问题
* 思考：对象在堆区的空间已经释放了,还能再使用p吗?

   ```objc
   Person *p = [[Person alloc] init];
   [p release];

   // 因为P已经被释放，此时调用p的run方法，此时会报错。
   // 我们把p叫做野指针，把p指向的对象叫做僵尸对象。
   [p run];
```
* 野指针错误:访问了一块坏的内存(已经被回收的,不可用的内存)。

* 僵尸对象:所占内存已经被回收的对象,僵尸对象不能再被使用。

* 注意:
 * __1> 空指针:没有指向任何东西的指针,给空指针发送消息不会报错.__

 * 关于nil和Nil及NULL的区别:
   * 1.nil: A null pointer to an Objective-C object. ( #define nil ((id)0) )
       * nil 是一个对象值。
       * Person *p = [Person new];
       * p = nil;

   * 2.Nil: A null pointer to an Objective-C class.
       * 如:Class someClass = Nil;给类对象赋值

   * 3.NULL: A null pointer to anything else. ( #define NULL ((void *)0) )
      * NULL是一个通用指针(泛型指针)。

   * 4.NSNull: A class defines a singleton object used to represent null values in collection objects (which don't allow nil values).
     * [NSNull null]: The singleton instance of NSNull。
     * [NSNull null]是一个对象,他用在不能使用nil的场合。

 * __2> 不能使用[p retain]让僵尸对象起死复生。__
 * __3> 不能对野指针进行操作__

#### 避免使用僵尸对象的方法

 * 为了防止不小心调用了僵尸对象,可以将对象赋值nil(对象的空值)
    * 给空指针发消息是没有任何反应的。
    ```objc
      Student *s = [[Student alloc] init];

      [s release];

      s = nil;

      // 打印对象的引用计数器值
    NSLog(@"%lu",[s retainCount]);
    ```

#### 对象的内存泄露

* 1.retain和release的个数不匹配，导致内存泄露。

* 2.对象使用的过程中被赋值了nil,导致内存泄露
![](/img/5.7.png)

* 3.在函数或者方法中不当的使用retain 或者 release 造成的问题
![](/img/5.8.png)
