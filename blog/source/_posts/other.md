---
title: Other
date: 2016-07-07 11:38:06
tags: Other
categories : "UI"
---

### 保存图片, 视频

```objc
//图片
UIImageWriteToSavedPhotosAlbum(self.imageView.image, self, @selector(image:didFinishSavingWithError:contextInfo:), nil);

//视频
UISaveVideoAtPathToSavedPhotosAlbum(<#NSString * _Nonnull videoPath#>, <#id  _Nullable completionTarget#>, <#SEL  _Nullable completionSelector#>, <#void * _Nullable contextInfo#>)

//图片保存结果的回调
//方法要有三个参数
//方法要有三个参数
- (void)image:(UIImage *)image didFinishSavingWithError:(NSError *)error contextInfo:(void *)contextInfo
{
    if (error) {
        [SVProgressHUD showErrorWithStatus:@"保存失败"];
    } else {
        [SVProgressHUD showSuccessWithStatus:@"保存成功"];
    }
}

视频保存结果的回调
- (void)video:(NSString *)videoPath didFinishSavingWithError:(NSError *)error contextInfo:(void *)contextInfo
{
    if (error) {
        [SVProgressHUD showErrorWithStatus:@"保存失败"];
    } else {
        [SVProgressHUD showSuccessWithStatus:@"保存成功"];
    }
}
```

### 解决TableView\CollectionView加载数据时多次刷新问题

```objc

解决多次刷新问题
方法1.定义属性parameters, 判读parameters是否相同
方法2.NSURLSessionDataTask的cancel方法
一个任务被取消,AFNetworking 会调用取消任务的 failure 的 block

//makeObjectsPerformSelector数组中的所有元素都执行Selector方法
    [self.manager.tasks makeObjectsPerformSelector:@selector(cancel)];

//控制器销毁时
- (void)dealloc
{
    //取消所有的任务
    [self.manager invalidateSessionCancelingTasks:YES];
    //or
    //停止所有操作
    [self.manager.operationQueue cancelAllOperations];

    //取消任务, 还能开起任务
    //[self.manager.tasks makeObjectsPerformSelector:@selector(cancel)];
    //invalidateSessionCancelingTasks=yes --> session 都无效,任务不能开启, cancel只是取消任务
}
```

### 拦截frame的修改

```objc
/**
 *  可以拦截所有对frame的修改
 */
- (void)setFrame:(CGRect)frame
{
    frame.origin.x = 10;
    frame.size.width -= 2 * frame.origin.x;
    frame.size.height -= 1;

    [super setFrame:frame];
}

/**
 *  可以拦截所有对bounds的修改
 */
- (void)setBounds:(CGRect)bounds
{
    [super setBounds:bounds];
}
```

### 控件无故拉伸问题

```objc
//如果设置了尺寸, 但控件的宽高拉伸, 可能就是UIViewAutoresizingNone
self.autoresizingMask = UIViewAutoresizingNone;
```

### 图片过大, 只全部显示图片头部

```objc
//开启图形上下文
UIGraphicsBeginImageContextWithOptions(post.pictureFrame.size, YES, 0.0);

//将下载的图片, 画到图像上下文中
//等比例缩放至宽或高全部显示后, 的图片frame
CGFloat imageW = post.pictureFrame.size.width;

CGFloat imageH = image.size.height * imageW / image.size.width;
[image drawInRect:CGRectMake(0, 0, imageW, imageH)];

//获取图片
self.imageView.image  = UIGraphicsGetImageFromCurrentImageContext();

//结束图形上下文
UIGraphicsEndImageContext();
```

### UI_APPEARANCE_SELECTOR

* 属性带有 UI_APPEARANCE_SELECTOR, 可以通过 appearance 统一设置

```objc
//eg:
UINavigationBar *navigationBar = [UINavigationBar appearance];
[navigationBar setBackgroundImage:[UIImage imageNamed:@"navigationbarBackgroundWhite"] forBarMetrics:UIBarMetricsDefault];
[navigationBar setTitleTextAttributes:@{NSFontAttributeName : [UIFont boldSystemFontOfSize:20]}];

//注意:
self.navigationItem.rightBarButtonItem.enabled = NO;
//使用UI_APPEARANCE_SELECTOR-->appearance时,分样式的设置会导致样式不会改变, 需要强制刷新
[self.navigationController.navigationBar layoutIfNeeded];
```

### 设置状态栏的样式

```objc
//Info.plist 配置 View controller-based status bar appearance : NO
[UIApplication sharedApplication].statusBarStyle = UIStatusBarStyleDefault;
```

### presentViewController

```objc
当一个控制器 model 出另一个控制器
[A presentViewController:B animated:YES completion:nil];
A.presentedViewController --> B
B.presentingViewController --> A
```
