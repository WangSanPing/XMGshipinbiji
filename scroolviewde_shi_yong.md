# UIScrollView的基本使用

- 用法
  1. 将需要展示的内容添加到UIScrollView中
  2. 设置UIScrollView的contentSize属性，告诉UIScrollView所有内容的尺寸，也就是告诉它滚动的范围(能滚多远，滚到哪里是尽头)


- 显示内容的小细节
  - 超出UIScrollView边框的内容会自动隐藏
  - 用户可以通过手势拖动来查看超出边框被隐藏的内容


- 注意点
  - 如果UIScroolView无法滚动，可能是以下原因：
    - 没有设置contentsize
    - scrollEnabled = NO
    - 没有接收到触摸事件 userInteractionEnable = NO


- UIScrollView的常见属性
  - @property(nonatomic) CGPoint contentOffset;
    - 这个属性用来表示UIScrollView滚动的位置（内容左上角于scrollview左上角的间距值）
  - @property(nonatomic) CGSize contentSize; 
    - 这个属性用来表示UIscrollview内容的尺寸，滚动范围。
  - @property(nonatomic) UIEdgeInsets contentInset
    - 这个属性能够在UIScrollView的四周增加额外的滚动区域，一般用来避免scrollView的内容被其他控件挡住



