# 按钮控制及数据存取


##数据存取的几个注意点

- 如有成对的数据出现最好使用字典数组
- 定义字典数组的方法如下：
```objc
NSArray *shops = @[
                   @{
                       @"icon" : @"danjianbao",
                       @"name" : @"单肩包"
                       },
                   @{
                       @"icon" : @"liantiaobao",
                       @"name" : @"链条包"
                       },
                   @{
                       @"icon" : @"qianbao",
                       @"name" : @"钱包"
                       },
                   @{
                       @"name" : @"手提包",
                       @"icon" : @"shoutibao.png"
                       },
                   @{
                       @"name" : @"双肩包",
                       @"icon" : @"shuangjianbao.png"
                       },
                   @{
                       @"name" : @"斜挎包",
                       @"icon" : @"xiekuabao.png"
                       }
                   ];
```
- 删除控件的方法：
```objc
  //删除当前subviews中的最后一个
    [[self.shopsView.subviews lastObject] removeFromSuperview];
```
##按钮控制
- 按钮控制的属性为enabled
```objc
    //可用
    self.addBtn.enabled = YES
```


![icon](http://7xrpl5.com1.z0.glb.clouddn.com/16-3-10/97102257.jpg)