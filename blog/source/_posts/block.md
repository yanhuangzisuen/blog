---
title: Block
date: 2016-07-07 11:39:06
tags: Block
categories : "Objective-C"
---

### 1、什么是block？
   * block是iOS中一种比较特殊的数据类型。
   * block是苹果官方特别推荐使用的数据类型，应用场景比较广泛。

### 2、使用场合？
    * 1）动画
    * 2）多线程
    * 3）集合遍历
    * 4）网络请求回调
###3、block的作用
    * 用来保存一段代码，可以在恰当的时间再取出来调用.


## block的基本用法
### 1）简单的认识下block
  * 函数写法：
  ```objc
   void myBlock (){
    NSLog(@“******”);
    NSLog(@“******”);
    NSLog(@“******”);
    NSLog(@“******”);
  }
  ```
  * block写法：
```objc
void (^myBlock)() =  ^{
  NSLog(@“******”);
  NSLog(@“******”);
  NSLog(@“******”);
  NSLog(@“******”);
}；
myBlock();
```
  * block格式：
  ```objc
  void (^block名称)(参数列表) = ^(参数列表){
  // 代码实现；
  }
```
##### 2）定义block遍历，存储一段代码，这段代码的功能是能打印任意行数
```
void (^ myBlock)(int) = ^(int numberOfLines){
  for(int i = 0; i < numberOfLines ; i ++){
     NSLog(@“******”);
    }
  }
```
##### 3）定义block，计算两个整数的和.
```
int (^ sumBlock)(int,int) = ^(int num1, int num2){
     return num1 + num2;
};
int c = sumBlock(10,20);
NSLog(@“%d”,c);
```
#####4）定义1个block，计算1个整数的平方
```
int (^squareBlock)(int);
squareBlock = ^(int sum){
   return sum * sum;
};
squareBlock(25);
```

## block的typedef

```objc
int ( ^minusBlock)(int,int) = ^(int num1,int num2){
  return num1 - num2;
};
```
* 定义1个叫做:MyBlock的数据类型，它存储的代码必须返回int，，必须接受2个int类型参数
```objc
typedef int(^MyBlock)(int,int);
```
* 重命名之后，可这样使用：
```objc
MyBlock minusBlock = ^(int num1,int num2){
  return num1 - num2;
};
```

##block访问外部变量

* 1）block访问外面变量。
```objc
int a = 10;
void (^block()) = ^{
  NSLog(@“%d”,a);
};
block();```
* 2）block修改外部变量值
```objc
__block int b = 10;
void (^block()) = ^{
 b = 20;
  NSLog(@“%d”,b);
};
block();
```
* 3）block的快捷操作，名称写完整，直接敲回车.


## block作为函数的返回值

* 1、使用typedef定义一个新的类型

```objc
//给block起一个别名
typedef int(^newType)(int num1,int num2);

```
* 2、使用新类型作为函数的返回值

```objc
//定义一个返回值是block类型的函数
newType test(){

//定义一个newType 类型的block变量
newType work1=^(int x,int y)
{
return x+y;
};
return work1;
}
```
* 3）定义变量接收函数返回的值(block类型)
* 4）调用block

```objc
//在main函数中调用返回值是newType类型的函数

// 定义block类型的变量n
newType n = test();

// 调用block，输出结果
NSLog(@"n = %d",n(10,20));
```

## block结构的快速提示
* 输入：`inlineBlock`
