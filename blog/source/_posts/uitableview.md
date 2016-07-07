---
title: UITableView
date: 2016-07-07 11:38:06
tags: UITableView
categories : "UI"
---

```objc
//有两个tableView不要调整inset
self.automaticallyAdjustsScrollViewInsets = NO;
```

## 分隔线样式
```objc
//没有分隔线
self.tableView.separatorStyle = UITableViewCellSeparatorStyleNone;
```

## tableView如何显示数据

```objc
tableView 中想要显示数据:
        遵守协议 : UITableViewDataSouse (决定数据)
        实现方法 :
            0.numberOfSectionsInTableView 一个 tableView 中有多少组
            1.numberOfRowsInSection 一组有多少行
            2.cellForRowAtIndexPath 每一行的内容
        调用的循序 :
            1.numberOfSectionsInTableView:
            2.numberOfRowsInSection: 会调用多遍, 上面的方法返回多少组就调用多少次
            3.cellForRowAtIndexPath: 总共有多少行, 就调用多少遍
```


```objc
/**
 *  告诉tableView一共有多少组数据
 */
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView

/**
 *  告诉tableView第section组有多少行
 */
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section

/**
 *  告诉tableView第indexPath行显示怎样的cell
 */
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath

/**
 *  告诉tableView第section组的头部标题
 */
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section

/**
 *  告诉tableView第section组的尾部标题
 */
- (NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section
```

### 静态单元格

* 静态单元格:

    一般数据不发送改变
    一定要在 UITableViewController 中使用
    只是相对于动态, cell 中的内容少, 而且不经常改变
    如果静态单元格, 实现了对应的数据源方法, 依然会走代码, 代码的组数, 行数只能比 storyboard 中的少, 不能多

* 动态单元格:

    里面的数据根据动态来加载 (plist,服务器)

**如果storyboard 设置了静态单元格, 而又实现了这3个数据源方法, 会清空storyboard的数据,
但是组数与行数与storyboard设置的不一致, 导致奔溃**
