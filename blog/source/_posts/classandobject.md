---
title: 类与对象
date: 2016-07-07 11:39:06
tags: object
categories : "Objective-C"
---

**对象:**某一个具体的存在

**类:**具有相似内部状态和运动规律的实体的集合. 具有相同属性和行为事物的统称
##类的构成
1. 类的名称:类名
2. 类的属性:一组包含数据的属性
3. 类的方法:允许对属性包含的数据进行操作的方法

##创建一个对象
[NSObject new] 在内存的干的三件事
1. 在堆中开辟一段存储空间
2. 初始化成员变量(类声明大括号中的属性叫成员变量, 也叫实例变量)
3. 返回开辟空间的首地址

## #pragma mark的使用
1. ###### #pragma mark -
2. ###### #pragma mark 名称
3. ###### 如果你的标志没有出现在弹出菜单中,比如没有分割线出现,请再Xcode菜 单"Preferences..."中的 "Code Sense" 选项取消选中“Sort list alphabetically”即可

### 类方法

    类方法中可以直接调用类方法
    类方法中不可以直接调用对象方法
    类方法中不能访问成员变量

### self
`不能在对象方法或类方法中利用self调用当前self所在的方法`

    如果self在对象方法中,那么self就代表调用当前对象方法的那个对象
    如果self在类方法中,那么self就代表调用当前类方法的那个类;
    总结:
    我们只有关注self在类方法中,还是在对象方法中,在类方法中,代表当前类,在对象方法中代表"当前调用该方法的对象"


### super

* 概念:

    super是编译器的指令符号,只是告诉编译器在执行的时候,去调用谁的方法
* 作用:

    1.直接调用父类的某个方法

    2.super在对象方法中,那么会调用父类的对象方法

    3.super在类方法中,那么会调用父类的类方法

### 继承

* 继承:

    A类继承B类,那么A累就用于B类所有的属性及方法

* 优点:

    1.提高代码的复用性

    2.可以让类与类产生关系,正是因为继承让我们的类与类之间产生关系,所有才有了多态

* 注意:

    千万不要以为继承可以提高代码的复用性,但凡发现多个类当中有复用的代码就抽取一个父类

    只有满足一定的条件我们才能够使用继承

    条件: XXX 是 XXX 或者 某某 is a 某某
        Iphone 继承 Phone  Iphone is a Phone

缺点:

    耦合性太强(依赖性太强)

### 多态

* 多态:

    事物多种表现形态

* 表现:

    父类的指针指向子类的对象

* 优点:

    提高代码的扩展性

* 注意点:

    如果父类指针指向子类对象,如果需要调用子类特有的方法,必须强制类型转换才能调用


### 实例变量修饰符

 @public
 >可以在其他类中访问被 @public 修饰的成员变量

 >也可以在本类中访问被 @public 修饰的成员变量

 >可以在子类类中访问父类中被 @public 修饰的成员变量

 @private
 >不可以在其他类中访问被 @private 修饰的成员变量

 >可以在本类中访问被 @private 修饰的成员变量

 >不可以在子类中访问父类中被 @private 修饰的成员变量

 @protected
 >不可以在其他类中访问被 @protected 修饰的成员变量

 >可以在本类中访问被 @protected 修饰的成员变量

 >可以在子类中访问父类中被 @protected 修饰的成员变量

 注意:默认情况下所有实例变量都是 @protected

 @package
 >介于 @public 和 @private 之间

 >如果在其他包中访问,那么是 @private

 >如果是在当前代码所在的包中访问就是 @public

 实例变量修饰符的作用域:从出现的位置开始,一直到下一个修饰符出现


### id - instancetype

1. instancetype == id == 万能指针 == 指向一个对象
2. instancetype在编译的时候可以判断对象的真实类型
3. id在编译的时候不能判断对象的真实类型
4. id 可以用来定义变量,可以作为返回值,可以作为形参
5. instancetype 只能用来作为返回值

`注意:自定义构造方法,返回值尽量使用instancetype,不要使用id`

### load - initialize

```objc
//load 一启动就调用,仅一次
//1.只有程序启动,就会将所有类的代码加载到内存中,放到代码区
//load方法会在当前类被加载到内存的时候调用,有且仅会调用一次
//如果有继承关系,先调用父类的load方法,在调用子类的load方法
+ (void)load
{
    NSLog(@"Person类被加载到内存了");
}

//initialize 一使用就调用,仅一次
//2.当当前类第一次被使用的时候就会被调用(创建类对象的时候)
//initialize 方法在整个程序的运行过程中只会被被调用一次  因为类对象只有一个
//initialize 用于对某个类进行 一次性 的初始化化
//如果有继承关系,先调用父类的initialize方法,在调用子类的initialize 方法
+ (void)initialize
{
    NSLog(@"Person类的initialize 方法");
}
```

### SEL 类型

* 是否响应该方法

```objc
- (BOOL)respondsToSelector:(SEL)aSelector;
```

* 调用该方法

```objc
//performSelector 最多只能传递两个参数
- (id)performSelector:(SEL)aSelector;
- (id)performSelector:(SEL)aSelector withObject:(id)object;
- (id)performSelector:(SEL)aSelector withObject:(id)object1 withObject:(id)object2;
```


### 野指针 - 空指针

* 野指针:

    当一个指针指向了一个"僵尸对象"我们就称这个指针为 野指针

    只有给一个野指针发送消息,就会报错

    *** -[Person release]: message sent to deallocated instance 0x100305ef0

    发送了一个消息给了一个已经释放的实例对象

* 空指针: nil 0 NULL

    为了避免给野指针发送消息会报错,一般情况下,当一个对象被释放后我们会将这个对象的指针设置为空指针

    在OC中给空指针发送消息不会报错
