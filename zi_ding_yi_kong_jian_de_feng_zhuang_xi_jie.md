# 自定义控件的封装细节

- ##### layoutSubviews的调用时刻
  - 当控件尺寸发生改变的时候回自动调用这个方法。
  - 需要注意的是iOS的调用机制是一种消息循环的机制，所以并不会每次设置frame的时候都调用，只会再最后一次设置frame的时候才会调用
    - 消息循环中会在时间段内会收集当前对view的修改，循环收集完成之后会一次性修改对view的操作。
- ##### 报错`CUICatalog:Invalid asset name supplide:(null)`该错误一般是因为当设置图片`[UIImage imageNamed:@"xxx"]`当设置的图片为空时会报该错误。
- 自定义控件的初始化调用的init方法
  - 通过纯代码创建的自定义控件会调用`-(instancetype)initWithFrame:(CGRect)frame`方法
  - 通过xib/storyboard创建自定义控件会调用`-(instancetype)initWithCoder:(NSCoder *)aDecoder`方法 NSCoder是Xib解析器
  - `-(void)awakeFromNib`也是通过xib/storyboard创建自定义控件时调用，不同的是该方法是当所有控件全部加载完成后才调用。而`-(instancetype)initWithCoder:(NSCoder *)aDecoder`不会，所以应该把希望对控件的控制放到该方法中
  - 当在写自定义控件需要对控件进行初始化设置时最好在`-(instancetype)initWithFrame:(CGRect)frame`方法和`-(void)awakeFromNib`方法中都写一次。