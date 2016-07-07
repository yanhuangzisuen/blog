---
title: UIApplication
date: 2016-07-07 11:38:06
tags: UIApplication
categories : "UI"
---

## UIApplication对象介绍
    * 对象主要用来保存一些数据和封装一些方法
    * 对象中的属性主要用来保存数据
    * 对象中的方法主要用来执行一些代码，即对象的一些行为

    * 如果接收到推送消息时，应用头像上的数字就是在应用级别上的操作。

    * 一个UIApplication代理一个应用程序，而且是单例的。
        * 用来封装整个应用程序的一个对象，比如当应用程序执行到某个时期要做什么，生命周期等。
    * 获取UIApplication对象,"[UIApplication sharedApplication];"(单例)

    sharedApplication : 返回应用程序的单例对象
        openURL : 可以打电话, 发邮件, 应用程序之间的跳转
        keyWindow : 应用程序的主窗口
        networkActivityIndicatorVisible : 在状态栏显示网络旋转的齿轮
        applicationIconBadgeNumber : 应用头像上的数字
        applicationSupportsShakeToEdit : 默认 yes, 摇晃手机时, Undo Redo 按钮

    * 当一个iOS程序启动后，首先创建的第一个对象就是UIApplication对象;
    * 利用UIApplication可以做一些应用级别的操作。
        * 当qq有消息的时候右上角显示的消息条数。
            * iOS8以后要经过用户的允许才能设置通知。
            * 如果用户点击了不允许，就要手动到设置里面去进行配置。
        * 联网操作时，状态栏上的等待图表指示器。waiting图表
        * 利用UIApplication打开某个资源：
            * 系统会自动根据协议识别使用某个app打开
    * 通过UIApplication管理状态栏
        * 自从iOS7开始可以通过两种方式控制器状态栏的
            * 控制器：通过UIViewController管理

## UIApplicationDelegate介绍
    * 新建完项目后的那个AppDelegate文件，就是UIApplication的代理对象
        * 并且该代理对象已经被设置好了，无需我们手动设置了。
        * 在main函数中进行的设置

# AppDelegate 应用程序代理对象

* 应用程序代理对象，用来监听应用程序的执行过程

* 常用监听方法

```objc
//应用程序加载完毕
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    //可执行自定义操作
    return YES;
}

//应用程序失去焦点
- (void)applicationWillResignActive:(UIApplication *)application {
    //不接受用户交互
}

//应用程序进入后台
- (void)applicationDidEnterBackground:(UIApplication *)application {
    //双击home键课查看
}

//应用程序进入前台
- (void)applicationWillEnterForeground:(UIApplication *)application {
    //双击home键，选中程序的时候进入前台
}

//应用程序获取焦点
- (void)applicationDidBecomeActive:(UIApplication *)application {
    //接受用户交互
}

//应用程序销毁
- (void)applicationWillTerminate:(UIApplication *)application {
    //只有在直接双击home，销毁程序时在会调用
}

//应用程序接收到内存警告
- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    //当内存不足时，会收到系统的内存警告
}

```
