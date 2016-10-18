# 综合使用


##通过storyboard创建

- #####把项目中使用的图片放到`Assets.xcassets`中，即使包含文件夹在使用时也不用加入文件夹路径
- #####按钮需要改变type属性为`Custom`才能使用自定义属性
- #####控件具有tag属性，相当于id


##通过代码创建button

- #####创建方法如下
```objc
//可以指定创建类型
UIButton *btn = [UIButton buttonWithType:UIButtonTypeCustom];
等同于
UIButton *btn = [[UIButton alloc]init];
```
- #####设定按钮点击事件
```objc
[btn addTarget:self action:@selector(add) forControlEvents:UIControlEventTouchUpInside];

 - (void)add
{
    // 添加图片
    UIImageView *iconView = [[UIImageView alloc] init];
    iconView.image = [UIImage imageNamed:@"danjianbao"];
    iconView.frame = CGRectMake(0, 0, 50, 50);
    [self.shopsView addSubview:iconView];
    
    // 添加文字
    UILabel *label = [[UILabel alloc] init];
    label.text = @"单肩包";
    label.frame = CGRectMake(0, 50, 50, 20);
    label.font = [UIFont systemFontOfSize:11];
    label.textAlignment = NSTextAlignmentCenter;
    [self.shopsView addSubview:label];
}
```

- #####button的相关操作

```objc
    //新建一个按钮
    UIButton *btnTest = [[UIButton alloc]init];
    btnTest.titleLabel.font = [UIFont systemFontOfSize:16];//title字体大小  
    btnTest.titleLabel.textAlignment = NSTextAlignmentCenter;//设置title的字体居中  
    //指定按钮的位置及宽高
    btnTest.frame = CGRectMake(30, 30, 50, 50);
    //设置按钮显示的文字为test
    [btnTest setTitle:@"test" forState:UIControlStateNormal];
    //设置按钮文字颜色为蓝色
    [btnTest setTitleColor:[UIColor blueColor] forState:UIControlStateNormal];
    //给按钮添加点击事件
    [btnTest addTarget:self action:@selector(remove) forControlEvents:UIControlEventTouchUpInside];  
```






