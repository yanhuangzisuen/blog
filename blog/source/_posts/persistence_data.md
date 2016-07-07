---
title: 数据存储
date: 2016-07-07 11:38:06
tags: Persistence Data
categories : "UI"
---

###数据存储(数据持久化)

- 1> 介绍iOS数据存储的5种方式
- 2> 介绍应用沙盒(应用程序的文件夹)
 -  • 如何找到应用沙盒的路径？首先需要显示隐藏文件。
 -  • 点击前往->个人->资源库->Application Support->iPhone Simulator->7.1->里面全是应用沙盒
- 3> 应用沙盒怎么多文件夹保存，在哪个文件夹。介绍沙盒里的每一个文件夹。

###plist存储

-  把一些系统自带的OC对象生成pilst文件存储起来。
- 1> 了解数据存储：数据存储一般有两个操作，一个存，一个取。拖两个按钮，一个用来存，一个用来取
- 2> plist存储原理：
 - 只要有writeToFile的对象，就能进行plist存储，调用writeToFile就能自动生成plist格式的文件。
 - 一般常用的Foundation对象都有这个方法，数组，字典，字符串等
- 3> 如何写入到沙盒，需要获取沙盒路径。
 - 获取Documents路径
 - 拼接文件名，因为数据是写入到文件中，不是写入到文件夹中。路径之间通过/分开的，为了避免自己写/，会用stringByAppendingPathCompent，自动在文件夹与文件之间添加/。
- 4> 如何读取，存储是什么类型存储，读取出来也是什么类型，直接用存储的类型，解析文件就好，用ContentsOfFile解析。
- 5> 注意plist存储，不能存储自定义对象，会失败的。

### 偏好设置

- 1> 什么是偏好设置存储：就是保存一些基本的信息，账号，密码，状态。
- 2> 偏好设置原理：不需要关心文件名，直接通过NSUserDefaults操作，默认就存到偏好设置里面了。
 -  通过NSUserDefaults就能直接访问软件的偏好设置(Library/Preferences)
- 3> 怎么利用偏好设置存储?利用NSUserDefaults调用setObject:forKey存储。
 - 偏好设置底层实现原理：底层其实就是利用一个字典，存储一些键值对。
 - 偏好设置好处：能快速存储一些键值对，如果用字典去存储，还需要获取文件名比较麻烦。
 - 偏好设置坏处：不能及时存储，需要做同步操作，把内存中的数据同步到硬盘上。
- 4> 怎么利用偏好设置读取?和字典一样，根据刚刚存储的Key读取。

### 自定义对象归档(归档：数据存储)

```objc
- 1> 自定义对象如何归档：用NSKeyedArchiver,调用archiveRootObject:toFile:方法，需要传一个对象，自定义一个对象，传进去。

 - 会报错,说对象没有encodeWithCoder方法，说明归档的时候默认会调用这个方法，去实现这个方法。

 - 默认打不出encodeWithCoder，必须遵守NSCoding协议才能实现这个方法。

 - encodeWithCoder什么时候调用：对象归档时候调用

 - encodeWithCoder作用：告诉系统对象里的哪些属性需要归档，怎么去归档，根据一个key去归档，目的就是以后取的时候，也根据这个key去取数据。

- 2> 自定义对象如何解档:用NSKeyedUnarchiver,调用unarchiveObjectWithFile方法，需要传一个文件名。

 - 会报错,说对象没有initWithCoder方法，说明解档的时候默认会调用这个方法，去实现这个方法。

 - initWithCoder什么时候调用：对象解档时候调用

 - initWithCoder作用：告诉系统对象里的哪些属性需要解档，怎么去解档，根据之前存储的key去解档

 - initWithCoder是一个初始化方法，需要先初始化父类的，但是不能调用[super initWithCoder:],因为父类NSObject没有遵守NSCoding协议。

- 3> initWithCoder什么时候需要调用[super initWithCoder:]

 - initWithCoder原理:只要解析文件就会调用，xib,storyboard都是文件，因此只要解析这两个文件，就会调用initWithCoder。

 - 因此如果在storyboard使用自定义view,重写initWithCoder方法，一定要调用[super initWithCoder:]，因为只有系统才知道怎么解析storyboard，如果没有调用，就解析不了这个文件。
```
###二、 数据持久化

* /Users/...../Data/... 这个是沙盒路径
* /Users/...../Bundle/.... 这个是 Bundle 路径

    * 介绍"沙盒"下的目录结构
    1> Documents目录: 保存应用程序自己的数据（比如：游戏进度存档、软件的一些个人设置等）。通过 iTunes、iCloud 备份时, 会备份这个目录下的数据

    2> Tmp 目录: 存储一些其他临时数据, 系统磁盘空间不够, 手机重启时, 会自动清除这个目录的数据。无需程序员手动清除该目录中的数据.iTunes、iCloud 备份时, 不会备份这个目录下的数据。

    3> Caches 目录: 保存从网络上下载的文件（比如：听歌时的缓存、图片的缓存等），这个目录下的数据不会被自动删除，需要程序员自己实现清除目录数据功能。iTunes、iCloud 备份时, 不会备份这个目录下的数据。

    4> Preference目录: 保存通过"偏好设置"写入的数据。iTunes、iCloud 备份时, 会备份这个目录下的数据。


####"沙盒" -> "Sandbox"

```objc
//"沙盒"示例路径: /Users/Steve/Library/Developer/CoreSimulator/Devices/0C63A035-071E-4EFC-8718-C387A3F7E026/data/Containers/Data/Application/287DAF0F-B201-4EDA-9E8A-D1DEDD9C9135

//通过调用NSHomeDirectory();来获取沙盒的根目录。
NSString *sandboxPath = NSHomeDirectory();

//获取"沙盒"下的"Documents"的路径
//1> 方式一: 先获取"沙盒"根路径, 再获取Documents路径(拼接)。（不推荐, 因为一旦系统升级Documents目录名字变了就不能用了）
NSString *sandboxPath = NSHomeDirectory();
NSString *docPath = [sandboxPath stringByAppendingPathComponent:@"Documents"];

//2> 方式二:
//参考代码:
// NSUserDomainMask 代表从用户文件夹下找, 沙盒根路径。
     // YES 代表展开路径中的波浪字符“~”
NSArray *array =  NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);

// 在iOS中，只有一个目录跟传入的参数匹配(沙盒中只有一个Documents目录)，所以这个集合里面只有一个元素
NSString *documents = [array objectAtIndex:0];

NSLog(@"%@", documents);

//向"沙盒"中写入数据
NSArray *array = @[@"Bob", @"John", @"Steve"];
NSString *filePath = [docPath stringByAppendingPathComponent:@"data.plist"];
    [array writeToFile:filePath atomically:YES];
```
####从"沙盒"中读取数据
    1> 获取文件的路径

    2> 调用NSArray、NSDictionary的xxxWithContentsOfFile

    ** 总结: 使用对象: 仅仅是Foundation框架中的一些类, 比如: NSString\NSArray\NSDictionary\NSSet\NSNumber\NSData

    ** 总结: 调用对象的writeToFile \ xxxWithContentsOfFile 方法来实现。

####使用"偏好设置"来存储数据
- 本质上就是通过"plist"来存储数据, 但是使用起来更简单(无需关注文件、文件夹路径和名称)。

 - 通过"偏好设置"的方式读、写文件时, 路径在"沙盒根目录" -> "Library" -> "Preferences"

 - 使用步骤:
   - 1> 创建一个访问"偏好设置"目录的对象NSUserDefaults对象
   ```objc
    NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults]; // 获得单例对象
    ```
   - 2> 通过"键值对"方式存储数据
   ```objc
    [defaults setObject:@"value" forKey:@"key"];
    [defaults setInteger:100 forKey:@"age"];
    [defaults setBool:YES forKey:@"auto_login"];
   ```
   - 3> 同步, 将内存中的数据写入文件。
   ```objc
    [defaults synchronize];
    ```
    ** 注意: 如果不调用synchronize方法, 则由系统随机进行同步(什么时候同步不确定)。

    - 4> 从"偏好设置"中读取数据
    ```objc
    [defaults objectForKey:@"key"];
    [defaults boolForKey:@"key"];
    ```
    ** 使用"偏好设置"存储数据的不足: 数据只能存储在一个文件中, 不存储大批量数据(很多时候大批量数据要分多个文件存储)

####通过"plist"文件来保存数据
- 无法直接将一个对象保存到文件中。比如Person对象就没有writeToFile方法。

    * "归档"是一种可以把任何对象, 直接保存为文件的方式。(其中包括"归档"与"反归档（读档）")

    * 归档: 对象 -> 文件
    ```objc
    [NSKeyedArchiver archiveRootObject:person toFile:filePath];
    ```
    * 反归档(读档): 文件 -> 对象
    ```objc
    [NSKeyedUnarchiver unarchiveObjectWithFile:filePath];
    ```
    * 通过"归档"的方式能将任何遵守了NSCoding协议的"对象"存储到文件中

    * NSCoding协议的两个重要的方法:
     - 1> - (void)encodeWithCoder:(NSCoder *)aCoder;
             ** 作用: 对象归档时调用该方法（将对象写入文件时）.
             1> 说明哪些属性要存储

             2> 说明如何存储这些属性

             ** 示例代码:
             // 归档时调用该方法
             - (void)encodeWithCoder:(NSCoder *)aCoder
             {
                 [aCoder encodeObject:self.name forKey:@"name"];
                 [aCoder encodeInteger:self.age forKey:@"age"];
                 [aCoder encodeDouble:self.height forKey:@"height"];
             }

             // 通过调用NSKeyedArchiver的archiveRootObject方法来实现归档
             CZPerson *person = [[SteveZPerson alloc] init];
             person.name = @"JackMeng";
             person.age = 27;
             person.height = 1.75;

             // 获取沙盒路径
             NSString *sandBoxPath = NSHomeDirectory();
             // 获取Documents的路径
             NSString *docPath = [sandBoxPath stringByAppendingPathComponent:@"Documents"];
             // 获取文件路径
             NSString *filePath = [docPath stringByAppendingPathComponent:@"person.plist"];

             // 将对象person归档
             [NSKeyedArchiver archiveRootObject:person toFile:filePath];

     - 2> - (id)initWithCoder:(NSCoder *)aDecoder;
             ** 作用: 当从文件中解析对象时调用该方法.
             1> 说明哪些属性要解析（读取）

             2> 说明如何解析（读取）这些属性

             ** 示例代码:

             // 读档时调用该方法
             - (id)initWithCoder:(NSCoder *)aDecoder
             {
                 if (self = [super init]) {
                 self.name = [aDecoder decodeObjectForKey:@"name"];
                 self.age = [aDecoder decodeIntegerForKey:@"age"];
                 self.height = [aDecoder decodeDoubleForKey:@"height"];
             }
                return self;
             }

             // 获取沙盒路径
             NSString *sandBoxPath = NSHomeDirectory();
             // 获取Documents的路径
             NSString *docPath = [sandBoxPath stringByAppendingPathComponent:@"Documents"];
             // 获取文件路径
             NSString *filePath = [docPath stringByAppendingPathComponent:@"person.bin"];

             CZPerson *person = [NSKeyedUnarchiver unarchiveObjectWithFile:filePath];

             NSLog(@"name: %@, age: %ld, height: %f", person.name, person.age, person.height);

    * 如果父类中也有属性需要归档、读档, 在子类中必须调用super的相关方法。
     示例代码:
     ```objc
     @implementation SteveZStudent
         - (id)initWithCoder:(NSCoder *)aDecoder
         {
             if (self = [super initWithCoder:aDecoder]) {
                self.SNo = [aDecoder decodeObjectForKey:@"SNo"];
             }
             return self;
         }

         - (void)encodeWithCoder:(NSCoder *)aCoder
         {
             [super encodeWithCoder:aCoder];
             [aCoder encodeObject:self.SNo forKey:@"SNo"];
         }
     @end
    ```

#### 使用SQLite数据库存储, 当非常大量的数据存储时使用
#### 使用Core Data存储, 就是对SQLite的封装
- 1> 从iOS 5.0出现
- 2> 效率低下, 不需要懂SQL语句, 直接操作对象。

***** 使用Core Data存储, 就是对SQLite的封装 *****
***** 通过"网络"方式存储 *****


####一、拖拽文件夹到项目中的3种方式:
• 当把一个文件夹拖拽到项目中的时候可以选择是否创建真正的文件夹还是只创建Group

1. 黄色的文件夹（Group）(经常用在应用程序中)
－在编译打包到设备上运行时，不会建立文件夹，所有的文件都保存在mainBundle中
－文件查找效率高
－不允许文件重名

2. 蓝色的文件夹(经常用在游戏开发中)
－在编译打包到设备上运行时，会建立文件夹，所有的文件都会按照文件夹的位置放置
－文件查找效率低
－游戏中经常会有“关卡”“皮肤”
－允许重名

3. 白色bundle(经常用在第三方框架，包装独立的素材[音效])
－第三方框架中，会自己指定文件名，为了不和应用程序的产生冲突，例如：success.png
－可以支持重名
* 简单制作 Bundle 文件, 可以直接把资源放到一个文件夹下, 然后修改文件夹的后缀为.bundle
* 然后直接把 Bundle拖拽到项目中, 使用其中的图片的时候要加Xxx.bundle/aaa.png 才能正常显示图片。

####二、如何通过 iTunes 下载ipa 文件, 并从中提取素材
* ipa文件本质上就是一个zip文件，使用“实用归档工具”可以直接解压缩


####三、UIImage 使用的细节
如果要在代码中通过 [UIImage imageWithContentsOfFile:path]; 加载图片，图片不能放在 Images.xcassets 中

####四、通过 block 为自定义视图传值。
* 为自定义视图创建一个 block 属性（使用 copy）
* 当点击自定义视图中的按钮时, 把自定义视图中的数据回传给主窗口中的 Label
** 要说明的问题:

1> 如何通过 block 传值

2> 通过 block 传值的时候, 对于 self 控制器要使用__weak修饰, 然后再使用, 否则有内存问题。

3> 为什么 bock 属性要使用 copy 来修饰
* 原因: 默认如果在 block 中使用了外部变量, 那么数据是保存在栈区的, 当超出方法作用域后, 方法中的局部变量就释放了, 所以当调用 block 的时候, 方法中的局部变量已经释放, 所以就无法访问到了。通过使用 copy关键字, 在进行 block 赋值的时候, 把 block拷贝到了堆中存储, 所以当局部的方法被释放以后依然可以使用 block访问到原来方法中的变量。
* 注意:此处使用strong 也是可以的, 在 arc 下使用 strong 编译器会默认做一次以 copy。但语义上最好还是用 copy。在 mrc 下没有 strong 关键字，所以必须使用 copy。
