---
title: Autorelease注意事项
date: 2016-07-07 11:39:06
tags: MRC
categories : "Objective-C"
---

## 1、autorelease使用注意

#####1）并不是放到自动释放池中，都会自动加入到自动释放池
* 1.1） 因为没有调用autorelease方法，所以对象没有加入到自动释放池.
```objc
int main() {
   @autoreleasepool {
    Student *s = [[Student alloc] init];
    [s release]; // 正常释放
   }
  return 0;
 }

 ```
* 1.2）在自动释放池的外部发送autorelease不会被加入到自动释放池中。
```objc
int main(){
   @autoreleasepool {

   }
   // 发送autorelease消息的对象，放到制动释放池外部
   // 此时无法被自动释放
  Student *s = [[[Student alloc] init] autorelease];
  return 0;
 }
 ```
* 1.3）不管对象是在自动释放池里创建，还是自动释放池外创建，只要在自动释放池内写1个[s autorelease];s就会被放到自动释放池中，注意：autorelease是一个方法，且只有在自动释放池中使用才有效。
```objc
int main(){
     // 不管在自动释放池内部还是外部创建
     Student *s = [[Student alloc] init];
     @autoreleasepool{
         [s autorelease]; // 此时s加入到释放池
   }
   return 0;
 }
 ```
* 2）自动释放池的嵌套使用
 * 自动释放池是栈结构。
 * 栈：先进后出。后进先出，

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
               // 第一个池子，里面创建no的1学生
                Student *s = [[[Student alloc] init] autorelease];
                s.no = 1;
        @autoreleasepool {
                // 第二个池子，里面创建no2的学生
                   Student *s2 = [[[Student alloc] init] autorelease];
                   s2.no = 2;
            @autoreleasepool {
                // 第二个池子，里面创建no3的学生
                        Student *s3 = [[[Student alloc] init] autorelease];
                        s3.no = 3;
            }
        }
    }
    return 0;
}
```
  * 释放顺序：s3,s2,s1
* 3）自动释放池中不适合放占用内存空间较大的对象
 * 1> 尽量避免对大内存使用该方法，对于这种延迟释放机制，尽量少用
 * 2> 不要把大量循环操作放到同1个自动释放池中，这样会造成内存峰值的上升。

####2)、autorelease错误用法

* 1、连续调用多次autorelease。

```objc
    @autoreleasepool {

        Student *s = [[[Student alloc] autorelease] autorelease];// 调用了两次autorelease，对象过度释放。

    }
```

* 2、对象创建在释放池外，但是在释放池内进行autorelease后，在释放池外，又进行了release。

```objc
   int main(int argc, const char * argv[]) {

      Student *s = [[Student alloc] init];

      @autoreleasepool {

         [s autorelease];// 此时出池子后，对象可以被释放

      }
         [s release];// 对象被释放后再次调用释放，会出错。


    return 0;
 }
 ```
* 3、alloc之后调用了autorelease，之后又调用release。

```objc
  int main(int argc, const char * argv[]) {

     @autoreleasepool {

        Student *s = [[[Student alloc] init] autorelease];

     }
        [s release];


    return 0;
}
```
* 4、alloc之后调用release。

```objc
  int main(int argc, const char * argv[]) {

     @autoreleasepool {
   // 因为release没有返回值，所以这样调用是错误的。
        Student *s = [[[Student alloc] init] release];
     }

    return 0;
}
```


##2、autorelease的应用场景

##### 1、autorelease的应用场景

* 经常用来在类方法中快速创建1个对象。

```objc
// 声明实现一个类方法
 + (Student *)student
{
    // 在里面直接进行autorelease
    return [[[Student alloc] init] autorelease];
}
```

* 应用：

```objc
// 在自动释放池中使用类方法创建对象
@autoreleasepool{
 // 此时创建出来的对象不用关注释放问题。
  Student *s = [Student student];
}
```

* 错误写法：

```objc
 int main(){
 // 在自动释放池中使用类方法创建对象
 @autoreleasepool{

 }
 // 写在自动释放池外部将无法释放对象。
  Student *s = [Student student];
  reutrn 0;
 }
```

#####2、完善快速创建对象的方法

* 问题1：如果定1个GoodStudent，继承自Student,此时，还能使用类方法快速创建对象吗？

 * 解决方案：
   * 在类方法中使用id

   ```objc
   + (id)student
{
    return [[[Student alloc] init] autorelease];
}
```
`此时，返回的对象仍旧是Student.所以，应该用self，替代Student.`
* 问题2：用其他对象类型，接受自定义对象类型。
* 如：
        NSString *s = [Student student];
        NSLog(@"%lu",s.length);
`这段代码，编译时，不会报任何警告，但是运行时会直接崩溃。`
* 改进办法：

  ```objc
  //instancetype：可以动态判断返回的类型和接受的类型是否一致
  + (instancetype)student{

    return [[self alloc] init];
}
```
* 此时，编译器会警告
        NSString *s = [Student student];
        NSLog(@"%lu",s.length);
