---
title: 由reloadSctions引发的崩溃问题
date: 2017-02-23 17:50:56
tags:
---
   
## 现象
   
   使用UITableView时，对分组做展开操作调用reloadSections::引发崩溃。崩溃在main中，无法准确定位。崩溃log如下：
  
```
 Terminating app due to uncaught exception 'NSInternalInconsistencyException', reason: 'UITableView (<UITableView: 0x7f7f149e6a00; frame = (0 0; 414 588); clipsToBounds = YES; gestureRecognizers = <NSArray: 0x604000651fd0>;     layer = <CALayer: 0x604000622d00>; contentOffset: {0, 0}; contentSize: {414, 4395}; adjustedContentInset: {0, 0, 0, 0}>) failed to obtain a cell from its dataSource (<HSStockTableView: 0x7f7f13cb9c30; frame = (0 35; 414 588); tag = 46957; gestureRecognizers = <NSArray: 0x604000651e50>; layer = <CALayer: 0x604000622ce0>>)
```


## 原因

`failed to obtain a cell from its dataSource`获取cell失败，这个时候应该检查cell是否正确地从复用池中取出，问题多是出在`- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath;`方法中。



