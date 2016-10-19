# UIView


## UIView的常见属性
- NSArray *subviews
  - 所有的子控件
  - 数组元素的顺序决定着子控件的显示层级顺序(下标越大，越显示在上面)

## UIView的常见方法

- addSubview
  - 添加一个子控件
  - 使用这个方法添加的子控件会被塞到subviews数组的最后面。

- 可以使用下面的方法调整子控件在subview数组中的顺序

```objc
// 将子控件view插入到subviews数组的index位置
- (void)insertSubview:(UIView *)view atIndex:(NSInteger)index;

// 将子控件view显示到子控件siblingSubview的下面
- (void)insertSubview:(UIView *)view belowSubview:(UIView *)siblingSubview;
// 将子控件view显示到子控件siblingSubview的上面
- (void)insertSubview:(UIView *)view aboveSubview:(UI---View *)siblingSubview;

// 将子控件view放到数组的最后面，显示在最上面
- (void)bringSubviewToFront:(UIView *)view;
// 将子控件view放到数组的最前面，显示在最下面
- (void)sendSubviewToBack:(UIView *)view;
```

## UIView的位置及大小控制

- 控制控件位置及大小的属性是**frame**，传递的参数为**CGRect**类型的结构体
```objc
    /**
     *  以下代码的功能为创建一个位置为100，100宽度200高度300的label
     */
    UILabel *label = [[UILabel alloc]init];
    label.text = @"我是lable";
    label.backgroundColor = [UIColor whiteColor];
    label.frame = CGRectMake(100, 100, 100, 100);
    label.textColor = [UIColor blackColor];
    [self.view addSubview:label];
```


## UIView的位置属性

```objc
//控件矩形框在父控件中的位置和尺寸(以父控件的左上角为坐标原点)
@property(nonatomic) CGRect frame;

//控件矩形框在父控件中的位置和尺寸(以自己左上角为坐标原点，所以bounds的x,y一般为0)
@property(nonatomic) CGRect bounds;

//控件中点的位置(以父控件的左上角为坐标原点)
@property(nonatomic) CGPoint center;

```


## 关于添加了一个view之后却不显示的一种可能性
