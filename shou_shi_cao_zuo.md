# 手势操作

### 为了完成手势识别，必须借助于手势识别器----UIGestureRecognizer

* ### 利用UIGestureRecognizer，能轻松识别用户在某个view上面做的一些常见手势

  * UIGestureRecognizer是一个抽象类，定义了所有手势的基本行为，使用它的子类才能处理具体的手势
  * UITapGestureRecognizer\(敲击\)

  ```objc
    - (void)setUpTap{
      UITapGestureRecognizer *tap = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(tap:)];

      tap.delegate = self;

      [self.image addGestureRecognizer:tap];
    }

  -(void)tap:(UITapGestureRecognizer *)tap{
      NSLog(@"%s",__func__);
    }
  ```


* UIPinchGestureRecognizer\(捏合，用于缩放\)
* UIPanGestureRecognizer\(拖拽\)
* UISwipeGestureRecognizer\(轻扫\)
* UIRotationGestureRecognizer\(旋转\)
* UILongPressGestureRecognizer\(长按\)

