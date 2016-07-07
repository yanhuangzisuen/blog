---
title: UITableViewCell
date: 2016-07-07 11:38:06
tags: UITableViewCell
categories : "UI"
---

### cell的样式

```objc
UITableViewCellStyleDefault : 不显示 detailTextLabel

UITableViewCellStyleValue1 : detailTextLabel 显示在 textLabel 右侧

UITableViewCellStyleValue2 : 不显示imageView, textLabel居左显示, 颜色变蓝

UITableViewCellStyleSubtitle : 都显示, detailTextLabel 显示在 textLabel 下侧
```

### cell选中的样式

```objc
//没有选中样式
cell.selectionStyle = UITableViewCellSelectionStyleNone;

self.backgroundColor = ZXX_COLOR(244, 244, 244);

//    self.textLabel.textColor = ZXX_COLOR(78, 78, 78);
    //cell设置选中的样式为none , cell不会进入高亮状态, 设置高亮的属性都不会显示
//    self.textLabel.highlightedTextColor = ZXX_COLOR(219, 21, 26);

    self.selectedBackgroundView = [[UIView alloc] init];
```

### cell的插入和删除

```objc
cell 的删除和插入
        删除
        打开默认在左侧的删除按钮
        _tableView.editing = YES;
        滑动删除
        _tableView.editing = NO;
        还需要实现
        - (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath
        删除 cell 的步骤
            删除数据源中的对象
            刷新数据 [_tableView deleteRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationLeft];
        插入 cell 的步骤
            插入新数据到数据源数组中
            刷新数据 [_tableView insertRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationLeft];
```

```objc
#pragma mark -
#pragma mark - 决定那一行是可以被编辑
//决定那一行是可以被编辑的, 要打开 tableView 的编辑模式
- (BOOL)tableView:(UITableView *)tableView canEditRowAtIndexPath:(NSIndexPath *)indexPath {
    return YES;
}

//删除模式中, 点击减号弹出的 delete, 点击 delete 才会调用这个方法
//添加模式中, 点击加号就会调用这个方法
    /**
     UITableViewCellEditingStyle:3种模式
        UITableViewCellEditingStyleNone,
        UITableViewCellEditingStyleDelete,
        UITableViewCellEditingStyleInsert
     */
- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath {

}

#pragma mark -
#pragma mark - 设置删除按钮上面显示的文本
//设置删除按钮上面显示的文本
- (NSString *)tableView:(UITableView *)tableView titleForDeleteConfirmationButtonForRowAtIndexPath:(NSIndexPath *)indexPath {
    return @"咔嚓掉";
}

#pragma mark -
#pragma mark - 决定编辑模式
//决定编辑模式
- (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath {

    return UITableViewCellEditingStyleDelete;
}

```

#### 复制粘贴

```objc
#pragma mark -
#pragma mark - 决定那一行长按要不要显示复制粘贴选项
- (BOOL)tableView:(UITableView *)tableView shouldShowMenuForRowAtIndexPath:(NSIndexPath *)indexPath {
    return YES;
}

#pragma mark -
#pragma mark - 决定菜单栏上显示的名称
- (BOOL)tableView:(UITableView *)tableView canPerformAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(nullable id)sender {
    if (action == @selector(copy:) || action == @selector(paste:)) {

        return YES;

    } else {

        return NO;
    }
}

#pragma mark -
#pragma mark - 点击菜单中选项会调用这个方法
- (void)tableView:(UITableView *)tableView performAction:(SEL)action forRowAtIndexPath:(NSIndexPath *)indexPath withSender:(nullable id)sender {

    if (action == @selector(copy:)) {
        HeroModel *heroModel = self.dataArray[indexPath.row];

        //保存至剪贴板中
        [UIPasteboard generalPasteboard].strings = @[heroModel.icon, heroModel.name, heroModel.intro];

    } else if (action == @selector(paste:)) {

        //从剪贴板中读取
        HeroModel *heroModel = [[HeroModel alloc] init];

        NSArray *array = [UIPasteboard generalPasteboard].strings;

        heroModel.icon = array[0];
        heroModel.name = array[1];
        heroModel.intro = array[2];

        //更新数据源
        [_dataArray insertObject:heroModel atIndex:indexPath.row];

        //刷新数据
        [_tableView insertRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationLeft];
    }
}
```


###awakeFromXib
    一个类和 xib 关联之后, 初始化方法
###实例化方法调用顺序

- init 与 initWithFrame

 - 当实例化方法为 initWithFrame 时只调用 initWithFrame 方法
 - 当实例化方法为 init 时, 先调用 initWithFrame 方法, 再调用 init 方法

###双模型
    单一原则, 每一个类, 每一个模型, 管理一类事
###计算文本 size 的方法
- 字体的大小
```objc
//限定的 size
CGSize contentMaxSize = CGSizeMake(MAXFLOAT, MAXFLOAT);
//NSFontAttributeName : 字体的大小, 字体大小要与文本上设置的一致
NSDictionary *attributesDict = @{NSFontAttributeName : [UIFont systemFontOfSize: 17]}
返回值为 CGRect 类型 = [要计算的文本 boundingRectWithSize:限定 size optionsNSStringDrawingUsesLineFragmentOrigin  attributes: 字典 context:nil];
```

###设置 footerView 和 headerView 的注意事项
- frame 的有些属性设置后, 添加到 tableView 上后会进行修改
 - 解决方法, 创建一个 tempView ,将实际想操作的 view 添加到 tempView 上

###菊花 Activity Indicator View

- startAnimating
- stopAnimating

###alpha = 0 与 clear color 的区别

- alpha = 0, 透明的, 添加的子控件也将透明
- clear color, 没有颜色, 添加的子控件可以看到

###延迟执行方法

```objc
[self performSelector:<#(non null SEL)#> withObject:<#(nullable id)#> afterDelay:<#(NSTimeInterval)#>]
//GCD
dispatch_after……
```
