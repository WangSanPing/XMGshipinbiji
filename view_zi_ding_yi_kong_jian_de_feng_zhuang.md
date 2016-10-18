# View自定义控件的封装

- ####为什么要封装view
  - #####如果一个view内部的子控件比较多，一般会考虑自定义一个view，把它内部子控件的创建屏蔽起来，不让外界关心
  - #####外接可以传入对应的模型数据给view，view拿到模型数据后给内部的子控件设置对应的数据

- ####封装控件的基本步骤
  - #####新建一个类继承自`UIView`
  - #####在initWithFrame：方法中添加子控件，提供遍历构造方法

  ```objc
/**
 *  初始化
 *
 *  @param frame
 *
 *  @return WXShopView
 */
-(instancetype)initWithFrame:(CGRect)frame
{
    if(self = [super initWithFrame:frame])
    {

        //        self.backgroundColor = [UIColor orangeColor];

        // 添加图片
        UIImageView *iconView = [[UIImageView alloc] init];
        iconView.backgroundColor = [UIColor blueColor];
        [self addSubview:iconView];
        self.iconView = iconView;

        // 添加文字
        UILabel *label = [[UILabel alloc] init];
        label.backgroundColor = [UIColor redColor];
        label.font = [UIFont systemFontOfSize:11];
        label.textAlignment = NSTextAlignmentCenter;
        [self addSubview:label];
        self.nameLabel = label;
    }

    return  self;
}
  ```
  
  - #####在layoutSubviews方法中设置子控件的frame（一定要调用super的layoutSubviews）
  
  ```objc
/**
 *  控件大小改变事件
 */
  -(void)layoutSubviews
  {
      [super layoutSubviews];

      float shopW = self.frame.size.width;
      float shopH = self.frame.size.height;

      self.iconView.frame = CGRectMake(0, 0, shopW, shopW);
      self.nameLabel.frame = CGRectMake(0, shopW, shopW, shopH - shopW);
  }
  ```
  - #####增加模型属性，在模型属性的set方法中设置数据到子控件
  
  ```objc
  /**
 *  Shop的set方法
 *
 *  @param shop
 */
-(void)setShop:(Shop *)shop
{
    _shop = shop;

    self.iconView.image = [UIImage imageNamed:shop.icon];
    self.nameLabel.text = shop.name;
}
  ```


  - ####注意点
    - 使用initWithFrame初始化方法，因为在调用init方法之后系统会再调用initWithFrame方法
