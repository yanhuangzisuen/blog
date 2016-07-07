---
title: UILabel
date: 2016-07-07 11:38:06
tags: UILabel
categories : "UI"
---

### 字体

```objc
[UIFont boldSystemFontOfSize:<#(CGFloat)#>]//粗体
    //italicSystemFontOfSize:  斜体
```

### 富文本

```objc
NSString *commentString =[NSString stringWithFormat:@"回复 %@: %@", parentsComment.nick, _comment.content];

NSRange range = [commentString rangeOfString:parentsComment.nick];

NSMutableAttributedString *attString = [[NSMutableAttributedString alloc] initWithString:commentString];

[attString addAttribute:NSForegroundColorAttributeName value:[UIColor orangeColor] range:range];

self.label.attributedText = attString;
```

### 计算文本范围

```objc
CGSize textSize = CGSizeMake(限定宽度, MAXFLOAT);

CGRect textRect = [label.text boundingRectWithSize:textSize options:NSStringDrawingUsesLineFragmentOrigin attributes:@{NSFontAttributeName: [UIFont systemFontOfSize:15]} context:nil];
```

```objc
label.autoresizingMask = UIViewAutoresizingFlexibleHeight;
```


