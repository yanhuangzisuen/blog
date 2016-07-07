---
title: NSArray常见用法
date: 2016-07-07 11:39:06
tags: NSArray
categories : "Objective-C"
---

## NSArray 的检索

* 获取集合元素的个数

        - (NSUInteger)count;

* 获取 index 位置的元素

        - (id)objectAtIndex:(NSUInteger)index;

* 是否包含某一个元素

        - (BOOL)containsObject:(id)anObject;

* 返回第一个元素

        - (id)firstObject;

* 返回最后一个元素

        - (id)lastObject;

* 查找 anObject 元素在数组中的位置(如果找不到, 返回 -1)

        - (NSUInteger)indexOfObject:(id)anObject;

* 在 range 范围内查找 anObject 元素在数组中的位置

        - (NSUInteger)indexOfObject:(id)anObject inRange:(NSRange)range;

* 返回两个数组第一个相同的元素
        - (nullable ObjectType)firstObjectCommonWithArray:(NSArray<ObjectType> *)otherArray;

## 数组的简写形式

**自从2012年开始, Xcode的编译器多了很多自动生成代码的功能, 使得OC代码更加精简**

* 数组的创建

    ```objc
    //之前
    [NSArray arrayWithObjects:@"Jack", @"Rose", @"Jim", nil];
    //现在
    @[@"Jack", @"Rose", @"Jim"];
    ```
* 数组元素的访问

    ```objc
    //之前
    [array objectAtIndex:0];
    //现在
    array[0];
    ```

## NSArray 给所有元素发送消息

* 让集合中的所有元素都执行 aSelector 这个方法

```objc
- (void)makeObjectsPerformSelector:(SEL)aSelector;

- (void)makeObjectsPerformSelector:(SEL)aSelector withObject:(id)argument;
```

## 数组的排序

#### compare

```objc
NSArray *arr = @[@10, @1, @8, @6, @6, @19];
//compare  想使用compare 对数组进行排序,数组元素必须是Foundation 框架中的对象,不能是自定义对象
NSArray *newArr = [arr sortedArrayUsingSelector:@selector(compare:)];
```

#### 二分排序

```objc
Person *p1 = [[Person alloc] init];
Person *p2 = [[Person alloc] init];
Person *p3 = [[Person alloc] init];
Person *p4 = [[Person alloc] init];
p1.age = 20;
p2.age = 10;
p3.age = 40;
p4.age = 30;

NSArray *arr = @[p1, p2, p3, p4];
NSLog(@"排序前%@", arr);
//不能使用 compare 方法对自定义对象进行排序
//NSArray *newArr = [arr sortedArrayUsingSelector:@selector(compare:)];

//二分排序
NSArray *newArr = [arr sortedArrayWithOptions:NSSortStable usingComparator:^NSComparisonResult(Person *obj1, Person *obj2) {
    //每次调用该 block 都会取出数组中的两个元素 id  _Nonnull 可以改成 Person *
    //NSLog(@"obj1 = %@, obj2 = %@", obj1, obj2);
    return obj1.age > obj2.age;//升序
//  return obj1.age < obj2.age;//降序
//如果比较的属性为字符串,
return [obj1.name compare: obj2.name];//升序
//return [obj2.name compare: obj1.name];//降序
    }];
```

#### 排序描述器

* 可以按多个属性排

```objc
Person *p1 = [Person personWithName:@"c" andAge:23];
Person *p2 = [Person personWithName:@"a" andAge:21];
Person *p3 = [Person personWithName:@"b" andAge:20];
Person *p4 = [Person personWithName:@"b" andAge:19];

NSMutableArray *arr = [NSMutableArray arrayWithObjects:p1, p2, p3, p4, nil];

//创建排序描述器, ascending 升序
NSSortDescriptor *nameSortDesc = [NSSortDescriptor sortDescriptorWithKey:@"name" ascending:YES];
NSSortDescriptor *ageSortDesc = [NSSortDescriptor sortDescriptorWithKey:@"age" ascending:YES];

//进行排序
[arr sortUsingDescriptors:@[nameSortDesc, ageSortDesc]];
NSLog(@"%@", arr);
```

```objc
Car *c1 = [[Car alloc] init];
c1.name = @"BMW";

Car *c2 = [[Car alloc] init];
c2.name = @"Benz";

Car *c3 = [[Car alloc] init];
c3.name = @"MINI";

Car *c4 = [[Car alloc] init];
c4.name = @"BYD";

Person *p1 = [Person personWithName:@"zhangsan" andAge:21 andCar:c1];
Person *p2 = [Person personWithName:@"zhangsan" andAge:21 andCar:c2];
Person *p3 = [Person personWithName:@"lisi" andAge:19 andCar:c3];
Person *p4 = [Person personWithName:@"wangwu" andAge:18 andCar:c4];

//创建排序描述器
NSSortDescriptor *nameSortDesc = [NSSortDescriptor sortDescriptorWithKey:@"name" ascending:YES];
NSSortDescriptor *ageSortDesc = [NSSortDescriptor sortDescriptorWithKey:@"age" ascending:YES];

NSSortDescriptor *carSortDesc = [NSSortDescriptor sortDescriptorWithKey:@"car.name" ascending:YES];

NSMutableArray *arrM =[NSMutableArray arrayWithArray:@[p1, p2, p3, p4]];

[arrM sortUsingDescriptors:@[nameSortDesc, ageSortDesc, carSortDesc]];
NSLog(@"%@", arrM);

```
