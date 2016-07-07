---
title: UITextField
date: 2016-07-07 11:38:06
tags: UITextField
categories : "UI"
---

####返回textField的宽度

```objc
self.textField.width = [self.textField.text sizeWithAttributes:@{NSFontAttributeName : self.textField.font}].width;
```

### 富文本

```objc
 /*
    NSMutableDictionary *attributes = [NSMutableDictionary dictionary];

    attributes[NSFontAttributeName] = [UIFont systemFontOfSize:16];

    attributes[NSForegroundColorAttributeName] = [UIColor grayColor];

    //NSAttributedString : 带有属性的文字(富文本)
    NSAttributedString *placeholder = [[NSAttributedString alloc] initWithString:@"账号" attributes:attributes];

    self.phoneField.attributedPlaceholder = placeholder;
     */

    /*
    NSMutableAttributedString *placeholder = [[NSMutableAttributedString alloc] initWithString:@"手机号"];
    //NSMutableAttributedString 可以单个字设置属性
    [placeholder setAttributes:@{NSForegroundColorAttributeName: [UIColor whiteColor]} range:NSMakeRange(0, 1)];

    self.phoneField.attributedPlaceholder = placeholder;
     */
```

## UITextField 设置监听的3种方式:

##### 1> 通过addTarget方式

* UITextField继承UIControll,可以addTarget监听。
* 但是这种方式只能监听一些"单击事件"、"滚动条滚动事件"等, 有些事件通过addTarget方式监听无效, 比如"Value Changed"事件。

####2> 通过代理
* 文本框的代理协议"UITextFieldDelegate"。演示:textFieldShouldBeginEditing方法。

```objc
// 为某个文本框设置代理
- (void)viewDidLoad {
    [super viewDidLoad];
    // 设置文本框代理为当前控制器。
    self.textFidld.delegate = self;
 }

// 让当前控制器遵守UITextFieldDelegate协议, 并且实现- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField方法, 返回YES
- (BOOL)textFieldShouldBeginEditing:(UITextField *)textField
{
    return YES;
}
```


### 3> 通过"通知中心"监听事件。

** 思路: 让用户名、密码文本框同时设置监听到textChanged方法。

```objc
//参考代码:

- (void)viewDidLoad {
    [super viewDidLoad];
//通过通知中心监听文本框内容变化, 添加观察者
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(textFieldValueChanged) name:UITextFieldTextDidChangeNotification object:self.userNameTextField];

    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(textFieldValueChanged) name:UITextFieldTextDidChangeNotification object:self.passWordTextField];

//TextField通知名
//    UIKIT_EXTERN NSString *const UITextFieldTextDidBeginEditingNotification;
//    UIKIT_EXTERN NSString *const UITextFieldTextDidEndEditingNotification;
//    UIKIT_EXTERN NSString *const UITextFieldTextDidChangeNotification;
}

//实现监听方法
- (void) textFieldValueChanged
{
    //文本框的值发送改变, 就会调用
}

/**** 注意通过通知的方式注册事件, 需要在dealloc方法中移除 ****/
// 移除通知监听, 观察者被销毁时, 在观察着的dealloc方法中移除
- (void)dealloc
{
    //移除观察者
    [[NSNotificationCenter defaultCenter]removeObserver:self];
}

```

### Placeholder
* 文本框有占位符，提示用户输入什么。设置 placeholder

### Secure Text Entry
* 密码文本框是暗文，密码属于机密，不需要显示出来。设置文本框的"Secure Text Entry"属性

### Clear Button
* 当文本框输入文字，会显示清除按钮，提高用户体验。设置文本框的"Clear Button"属性


### Segue对象。
* 在xcode6.1下, 拖线时选择Segue的style为show, 等价于以前的push。

* 重新拖线（手动 Segue）, 从控制器 to 控制器。

```objc
//参考代码 :
[self performSegueWithIdentifier:@"login2contact" sender:@"Jack"];

//实现控制器的- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender方法。


- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
// Get the new view controller using [segue destinationViewController].
// Pass the selected object to the new view controller.
//    NSLog(@"%@",sender);
//获取目标控制器
    UIViewController * targetVC = segue.destinationViewController;

}

```

```objc
//performSegueWithIdentifier:sender:的执行过程
[self performSegueWithIdentifier:@"login2contacts" sender:nil];
//1> self是来源控制器，只能通过来源控制器来调该方法。
//2> 根据identifier去storyboard中找到对应的线，新建UIStoryboardSegue对象
//3> 设置Segue对象的sourceViewController（来源控制器）
//4> 新建并且设置Segue对象的destinationViewController（目标控制器）
//5> 调用- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender方法
//6> 执行跳转。
//** 具体跳转步骤:
//1> 通过segue对象的sourceViewController获取源控制器所在的导航控制器。
//2> 将segue的destinationViewControlelr压栈(push)进去。
```

### 提示框的弹出

```objc
//xcode7下
- (IBAction)logOutBtnClick:(id)sender
{
    UIAlertController * alert = [UIAlertController alertControllerWithTitle:@"确定注销吗?" message:nil preferredStyle:UIAlertControllerStyleActionSheet];

    UIAlertAction * okAction = [UIAlertAction actionWithTitle:@"确定" style:UIAlertActionStyleDestructive handler:^(UIAlertAction * _Nonnull action) {
    [self.navigationController popViewControllerAnimated:YES];
    }];

    UIAlertAction * cancel = [UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:nil];

    [alert addAction:okAction];

    [alert addAction:cancel];

    [self presentViewController:alert animated:YES completion:nil];
}
```

```objc
// xcode6

// 1. 弹出UIActionSheet对话框
UIActionSheet *sheet = [[UIActionSheet alloc] initWithTitle:@"确定要注销" delegate:self cancelButtonTitle:@"取消" destructiveButtonTitle:@"注销" otherButtonTitles:nil, nil];

//alertView 上添加一个 textField
/*
UIAlertViewStyleDefault = 0,
UIAlertViewStyleSecureTextInput,//安全的文本输入, 密码保护模式
UIAlertViewStylePlainTextInput,//普通的文本输入
UIAlertViewStyleLoginAndPasswordInput//两行输入,Login 和 Password
*/
alertView.alertViewStyle = UIAlertViewStylePlainTextInput;

//获取 alertView上的 textField
UITextField *textField = [alertView textFieldAtIndex:0];

[sheet showInView:self.view];

```


* UIActionSheet中的按钮点击事件

```objc
- (void)actionSheet:(UIActionSheet *)actionSheet clickedButtonAtIndex:(NSInteger)buttonIndex
{
    //buttonIndex 对应按钮的下标
}
```
### awakeFromNib
* awakeFromNib什么时候调用？xib加载完成的时候调用
* awakeFromNib的作用:从控件从xib加载完成之后，做一些初始化操作。
* 在layoutSubViews设置尺寸。
