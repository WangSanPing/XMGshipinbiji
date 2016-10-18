# 通过ScrollView实现图片缩放


- ##使用方法
  - 遵守`UIScrollViewDelegate`协议
  - 实现`-(UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView`方法
  - 返回要缩放的图片
    - minimumZoomScale 最小倍数
    - maximumZoomScale 最大倍数
    - 需要注意：该方法返回的类型为UIView，故能通过该方法实现所有控件的缩放
    - 需要缩放的控件必须是UIScrollView的子控件
 - 示例代码如下

```objc
@interface ViewController () <UIScrollViewDelegate>

@property (weak, nonatomic) IBOutlet UIScrollView *scrollView;

@property (weak, nonatomic) IBOutlet UIImageView *image;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    self.scrollView.contentSize = self.image.frame.size;
    
    self.scrollView.delegate = self;
    self.scrollView.minimumZoomScale = 0.2;
    self.scrollView.maximumZoomScale = 2.0;
//    NSLog(@"%@",NSStringFromCGPoint(self.scrollView.contentOffset));
}

/**
 *  ssss
 *
 *  @param sender ffff
 */
- (IBAction)Left:(id)sender {
    
    //    self.scrollView.contentOffset = CGPointMake(0, 0);
    
    NSLog(@"%@",NSStringFromCGPoint(self.scrollView.contentOffset));
    
    [UIView animateWithDuration:1 animations:^{
        self.scrollView.contentOffset = CGPointMake(0, self.scrollView.contentOffset.y);

    } completion:^(BOOL finished){
        if(finished)
        {
             NSLog(@"执行完毕");
        }
    }];
    
}

- (IBAction)Top:(id)sender {
    //    self.scrollView.contentOffset = CGPointMake(self.scrollView.contentOffset.x, 0);

    CGPoint offset = CGPointMake(self.scrollView.contentOffset.x, 0);
    [self.scrollView setContentOffset:offset animated:YES];
}

-(UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView
{
    return self.image;
}

@end
```

![效果图](http://7xrpl5.com1.z0.glb.clouddn.com/16-3-26/96472339.jpg )