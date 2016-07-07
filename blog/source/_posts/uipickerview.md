---
title: UIPickerView
date: 2016-07-07 11:38:06
tags: UIPickerView
categories : "UI"
---

## 1.数据选择控件介绍：
    * UIPickerView-显示一组或多组数据方便用户选择。
        * 在文本框中输入数据时，如果是比较固定的话，就可以让用户直接去滚动选择，不需要用户再去手动输入。

    * UIDatePicker-显示一个日期组件方便用户选择日期或时间。
        * 与UIPickerView类似，可以更好地提高用户体验，方便用户输入内容。

    * 在iOS 8中就比较少使用UIPickerView控件了。比如选择语言或者区域时用户的是UITableView了。

    * 控件作用：
        * 从指定的数据源中选择控件。
        * 通常以UITextField的inputView的形式出现（当选中某个文本框后，弹出键盘中显示该控件）

    * 注意：
        * 使用PickerView之前都需要指定数据源对象和代理对象
        * 需要使用的两个协议：
            * UIPickerViewDataSource 数据源协议
            * UIPickerViewDelegate   代理协议


## info.plist文件介绍
    * 将项目文件夹用记事本打开，查看配置信息
    * 显示各项配置信息
    * 第一个文件夹保存项目中所有的相关内容。
    * Test文件夹主要是坐单元测试的时候用的，暂时没有用到，所以先不考虑
    * info.plist文件中保存了当前项目的所有配置。
        * 文件本身是一个xml文件，标记语言。
        * 在项目中配置的信息最后保存到info.plist文件中了。
        * 应用版本号
        * 应用要求的可运行的最低系统版本号
        * Main的storyboard

######  注意：自己创建的plist文件中不要包含Info关键字。

    * 在Xcode 5中名称为"项目名称-Info.plist"名称，Xcode6 以后就直接就是info.plist了。
    * bundle display name 应用名称的key，名称如果太长就不能完全显示了。
    * bundle identifier 应用的唯一标示，如果相同就会被覆盖。
    * bundle versions String short 最终应用发布时的版本号
    * bundle version 针对内部的一个版本号。
    * Supported interface ortations 标识设备所支持的方向，对应的选中"项目"->"General"->"Deployment Info"->"Device Orientation"。iPhone只支持3种方向，不支持上下颠倒的旋转，Portrait（竖屏），Landscape Left（横屏向左），Landscape Right（横屏向右）

    * Info.plist就是一个xml文件，可以通过open as source code 查看

## pch文件 "Prefix Header File（头文件）"
    * 在Xcode 6以后苹果就不推荐使用了。
    * 遇到的问题：
        * 整个项目中很多地方都在使用某个类的头文件
        * 整个项目中很多地方都在使用同一个"宏"
        * 在项目中很多地方都用到了NSLog（）方法，想一下子全部清除掉
    * 解决以上问题，可以通过使用PCH文件，它也是个头文件类似于*.h文件
###### 注意：PCH文件的特点，项目中所有其他代码文件无序显示导入该PCH文件，默认就可以访问（其他文件无序手动#import该PCH文件就能使用）

    * 主要作用：
        * 可以做一些公用的宏定义
        * 把公共的Model类的#import导入写到pch文件.
        * 自定义NSLog()。例如:#define ZXXLog(...) NSLog(__VA_ARGS__)

    *  创建pch文件
        * "newFile"->""->""
        * 将通用的头文件和相应的宏放进去。
    *  配置头文件，以使用头文件
        * 选择"项目"->"Build Setting" ->"All"->搜索 "Prefix Header",配置相应的pch文件。
        * "$(SRCROOT)/$(PRODUCT_NAME)/PrefixHeader.pch"（如果有问题，更换为下面的方式，可能会与中文有关）
        * "$(SRCROOT)/对应的文件夹名/PrefixHeader.pch"

    * 在应用程序测试的时候，需要log很多信息，但是如果我们发布程序的时候就要禁止打印信息。
        * 自定义自己的log方式。
        * 自定义log的完整形式
```objc
#ifdef DEBUG

#define ZXXLog(...) NSLog(__VA_ARGS__)

#else

#define ZXXLog(...)

#endif
```

    * 在使用pch文件时的注意点：
        * 创建c语言文件进去，直接编译就报错，因为默认情况下所有文件都会包含pch文件中的OC内容，C语言文件内不能识别OC代码，所以就会报错。
        * 解决：在pch文件中判断一下，如果是OC文件菜引入响应的宏，如果是普通C语言文件则不引入，否则项目中添加C语言文件时会报错。

```objc
#ifdef __OBJC__

// OC相关的内容

#endif
```

