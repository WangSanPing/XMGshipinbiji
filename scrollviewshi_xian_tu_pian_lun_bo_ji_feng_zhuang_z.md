# ScrollView实现图片轮播及封装自定义控件
####效果

![图片轮播](http://7xrpl5.com1.z0.glb.clouddn.com/16-3-29/97850421.jpg)
###步骤
1. 新建xib文件
2. 在xib文件中添加UIScrollView及UIPageControl
3. 新建类，把xib文件的Custom Class设置为该类
4. 在类中创建UIScrollView、UIPageControl两个控件变量和一个数组，数组用于存放图片名称。
5. 新建类方法返回该Xib文件
    
```objc
 /**
 *  初始化
 *
 *  @return 返回WXPageView
 */
+(instancetype)PageView
{
    return [[[NSBundle mainBundle] loadNibNamed:NSStringFromClass(self) owner:nil options:nil] lastObject];
}
    ```
6.在数组变量的set方法中给UIScrollView控件添加图片，并且设置UIPageControl的总页数(总页数即为图片总数)   

```objc
-(void)setImageNames:(NSArray *)imageNames
{
    _imageNames = imageNames;
    
    for (int i = 0; i < imageNames.count; i++) {
        UIImageView *imageView = [[UIImageView alloc]init];
        imageView.image = [UIImage imageNamed:imageNames[i]];
        
        [self.scrollView addSubview:imageView];
    }
    
    self.page.numberOfPages = imageNames.count;
}
```
7.重写layoutSubviews方法设置xib文件中所有控件的Frame。
```objc
-(void)layoutSubviews
{
    [super layoutSubviews];//注意不要忘记调用父类的layoutSubviews
    
    for (int i = 0; i<self.scrollView.subviews.count; i++) {
        self.scrollView.subviews[i].frame = CGRectMake(i * self.frame.size.width, 0, self.frame.size.width, self.frame.size.height);
    }
    
    self.scrollView.pagingEnabled = YES;
    self.scrollView.frame = CGRectMake(0, 0, self.frame.size.width, self.frame.size.height);
    // 图片宽度于scrollview一致，设置contentSize的X为总页数(即图片总数)乘以scrollview的宽度。不需要上下滚动，Y为0。
    self.scrollView.contentSize = CGSizeMake(self.page.numberOfPages * self.frame.size.width, 0);
    // 代理
    self.scrollView.delegate = self;
    // self.scrollView.frame.size.width / 2 是scrollView的X中心点
    // self.scrollView.frame.size.height / 2 是scrollView的Y中心点
    // (self.scrollView.frame.size.height / 2) + self.scrollView.frame.size.height / 3 是从Y的中心点算起再加上三分之一的scrollView高度
    self.page.frame = CGRectMake((self.scrollView.frame.size.width / 2) - 20, (self.scrollView.frame.size.height / 2) + self.scrollView.frame.size.height / 3, 50, 20);
}
```
8.实现UIScrollViewDelegate协议的scrollViewDidScroll方法，监听scrollview的滚动
```objc
-(void)scrollViewDidScroll:(UIScrollView *)scrollView
{
    //当前页等于scrollview的contentOffset.x除以scrollview的宽度再四舍五入
    int page = self.scrollView.contentOffset.x / self.scrollView.frame.size.width + 0.5;
    self.page.currentPage = page;
}
```
9.最后在用到该自定义控件的时候如下方法调用
```objc
    PageView *page = [PageView PageView];
    //只传图片名称
    page.imageNames = @[@"img_00",@"img_01",@"img_02",@"img_03",@"img_04"];
    page.frame = CGRectMake(20, 100, 374, 157);
    
    [self.view addSubview:page];
```

###~~现存问题：自定义控件中的UIPageControl位置没想到太好的办法调整，如果设置的宽度太高下面留余太多。~~

### 2016-3-31更新解决UIPageControl位置问题，改变计算位置方法如下
```objc
    // 获得scrollview的尺寸
    CGFloat scrollW = self.scrollView.frame.size.width;
    CGFloat scrollH = self.scrollView.frame.size.height;
    
    // 设置pageControl
    CGFloat pageW = 150;
    CGFloat pageH = 40;
    CGFloat pageX = scrollW - pageW;
    CGFloat pageY = scrollH - pageH;
    self.page.frame = CGRectMake(pageX, pageY, pageW, pageH);
```

##### 小贴士：如在设计接口时希望不再使用以前设计的方法，可以在属性后加`NS_DEPRECATED_IOS(2_0, 3_0)`，会在调用时显示删除线，即不再推荐该属性,还可以在NS_DEPRECATED_IOS(2_0, 3_0)后加文字推荐，例如:`NS_DEPRECATED_IOS(2_0, 3_0,"推荐使用XXX")`，其中2_0,3_0的意思是iOS2.0版本开始使用，3.0版本过期。