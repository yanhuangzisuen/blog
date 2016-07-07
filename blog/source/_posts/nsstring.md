---
title: NSString
date: 2016-07-07 11:39:06
tags: NSString
categories : "Objective-C"
---
## NSString创建方法

* 1.直接创建字符串:

```objc
NSString *str1 = @"ZXX";
NSString *str2 = @"ZXX";
//输出地址相同
NSLog(@"str1-%p", str1);
NSLog(@"str2-%p", str2);
```

* 2.格式化(凭借)字符串(堆区):

```objc
NSString *str1 = [NSString stringWithFormat:@"ZXX"];
NSString *str2 = [NSString stringWithFormat:@"ZXX"];
//输出地址不同
NSLog(@"str1-%p", str1);
NSLog(@"str2-%p", str2);
```

* 3.转换C语言字符串

```objc
char *str1 = "ZXX";
NSString *str2 = [NSString stringWithUTF8String:str1];
//输出地址不同
NSLog(@"str1--%p--%s",str1,str1);
NSLog(@"str2--%p--%@",str2,str2);
```

* 4.从文件在读取:

    * 4.1编码:

    英文:iso-8859-1

    中文:GB2312 < GBK < GB18030  汉字多少

    * 4.2将字符串写入文件
    ```objc
    NSString *content = @"ZXX";
    NSError *error = nil;
    // 注意：此时的one文件夹必须存在，否则写入失败。
    // 如果one文件夹存在，write.txt会自动被创建。
    [content writeToFile:@"/Users/yan/Desktop/one/write.txt" atomically:YES encoding:NSUTF8StringEncoding error:&error];
    if (error != nil) {
        NSLog(@"错误信息：%@",error.localizedDescription);
    }else{
        NSLog(@"恭喜！写入成功！");
    }
    ```
    * 4.2从文件中读取字符串

    ```objc
    NSError *error = nil;
    NSString *readFile = [NSString stringWithContentsOfFile:@"/Users/yan/Desktop/readFile.txt" encoding:NSUTF8StringEncoding error:&error];

    if (error == nil) {
        NSLog(@"%@",readFile);
    }else{
        NSLog(@"%@",error.localizedDescription);
    }
    ```
