---
title: UIMenuController
date: 2016-07-07 11:38:06
tags: UIMenuController
categories : "UI"
---

```objc
#pragma mark -
#pragma mark - UIMenuController的处理
- (void)didClickCell
{
    UIMenuController *menu = [UIMenuController sharedMenuController];

    if (menu.isMenuVisible) {

        [menu setMenuVisible:NO animated:YES];

    } else {
        [self becomeFirstResponder];

        UIMenuItem *dingItem = [[UIMenuItem alloc] initWithTitle:@"顶" action:@selector(ding:)];
        UIMenuItem *replyItem = [[UIMenuItem alloc] initWithTitle:@"回复" action:@selector(reply:)];
        UIMenuItem *reportItem = [[UIMenuItem alloc] initWithTitle:@"举报" action:@selector(report:)];
        [menu setMenuItems:@[dingItem, replyItem, reportItem]];

        CGRect rect = CGRectMake(0, self.height * 0.5, self.width, self.height * 0.5);
        [menu setTargetRect:rect inView:self];
        [menu setMenuVisible:YES animated:YES];
    }
}

/**
 *  能能成为第一响应者
 */
- (BOOL)canBecomeFirstResponder
{
    return YES;
}

/**
 *  能响应对应的事件
 */
- (BOOL)canPerformAction:(SEL)action withSender:(id)sender
{
    if (action == @selector(ding:) || action == @selector(reply:) || action == @selector(report:)) {
        return YES;
    }
    return NO;
}

/**
 *  顶
 */
- (void)ding:(UIMenuController *)menu
{
    ZXX_SHOW_METHOD_INFO
}

/**
 *  评论
 */
- (void)reply:(UIMenuController *)menu
{
    ZXX_SHOW_METHOD_INFO
}

/**
 *  举报
 */
- (void)report:(UIMenuController *)menu
{
    ZXX_SHOW_METHOD_INFO
}
```

### block 调用时防错处理

```objc
- (void)clickButtonWithCompletionBlock:(void(^)())completionBlock
{
    //...
    //当外界调用该方法传block 为 nil 时, 直接调用会出错
    //要判断
    !completionBlock ? : completionBlock();
}
```
