# 九宫格计算

- #####列号的计算方法为*当前要添加的位置索引和总列数取模(求余)*
- #####行号的计算方法为*当前要添加的位置索引和总列数取商(除法)*
- ####计算思路
  - 利用控件的索引index计算出控件所在的行号和列好
  - 利用列号计算控件的x值
  - 利用行号计算控件的y值


```objc
- (void)add
{
    
    //定义容器的宽
    CGFloat shopW = 50;
    //定义容器的高
    CGFloat shopH = 70;
    //指定列数
    int clos = 3;
    //计算列间距(整体宽度减掉列数乘以单个容器的宽度再除以列数减一)
    CGFloat cloMargin = (self.shopsView.frame.size.width - clos * shopW) / (clos - 1);
    //行间距
    CGFloat rowMargin = 10;
    //索引
    NSUInteger index = self.shopsView.subviews.count;
    //列数(取模)
    NSInteger col = index % clos;
    //x坐标值(当前列数乘以容器的宽加列间距)
    CGFloat shopX = col * (shopW + cloMargin);
    
    //行数(取商)
    NSInteger row = index / clos;
    //y坐标值(当前列数乘以容器的高加行间距)
    CGFloat shopY = row * (shopH + rowMargin);
    
    UIView *shopView = [[UIView alloc] init];
    shopView.backgroundColor = [UIColor redColor];
    
    // 添加图片
    UIImageView *iconView = [[UIImageView alloc] init];
    iconView.image = [UIImage imageNamed:@"danjianbao"];
    iconView.frame = CGRectMake(0, 0, 50, 50);
    [shopView addSubview:iconView];
    
    // 添加文字
    UILabel *label = [[UILabel alloc] init];
    label.text = @"单肩包";
    label.frame = CGRectMake(0, 50, 50, 20);
    label.font = [UIFont systemFontOfSize:11];
    label.textAlignment = NSTextAlignmentCenter;
    [shopView addSubview:label];
    
    shopView.frame = CGRectMake(shopX, shopY, shopW, shopH);
    [self.shopsView addSubview:shopView];
}

```