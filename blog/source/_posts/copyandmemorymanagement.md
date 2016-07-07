---
title: Copy与内存管理
date: 2016-07-07 11:39:06
tags: Copy
categories : "Objective-C"
---

#### 1、copy与内存管理

 * copy一次，retainCount +1

#### 2、深浅拷贝总结

 * 深复制（深拷贝，内容拷贝，deep copy）
   * 源对象和副本对象是不同的两个对象,源对象引用计数器不变, 副本对象计数器为1（因为是新产生的）
   * __本质是：产生了新的对象__

 * 浅复制（浅拷贝，指针拷贝，shallow copy）
   * 源对象和副本对象是同一个对象，源对象（副本对象）引用计数器 + 1, 相当于做一次retain操作
   * __本质是：没有产生新的对象__

#### 3、@property中的copy作用

```objc
//创建可变字符串
NSMutableString *str = [NSMutableString string]; //设定字符串的内容
str.string = @"zhangsan";
//创建对象
Person *person = [Person new]; //给person的实例变量赋值 person.name = str;
//修改字符串内容
[str appendString:@"xxxx"];
NSLog(@"name = %@",person.name); NSLog(@"str = %@",str);
// 输出结果：
//name = zhangsanxxxx
//str = zhangsanxxxx

//这显然不符合我们的要求,因为str修改后,会影响person.name 的值 解决方法:
@property (nonatomic,copy) NSString *name;
set方法展开形式为:
- (void)setName:(NSString *)name
{
  if (_name != name) {
    [_name release];
    [_name release];
    _name = [name mutableCopy];
    }
}
```

#### 2、【理解】@property内存管理策略选择
* @property内存管理策略的选择
 * 1.非ARC
    * 1> copy : 只用于NSString\block
    * 2> retain : 除NSString\block以外的OC对象
    * 3> assign:基本数据类型、枚举、结构体(非OC对象),当2个对象相互引用,一端用retain,一端用assign
 * 2.ARC
    * 1> copy : 只用于NSString\block
    * 2> strong : 除NSString\block以外的OC对象
    * 3> weak : 当2个对象相互引用,一端用strong,一端用weak
    * 4> assgin : 基本数据类型、枚举、结构体(非OC对象)
