# 给ScrollView添加定时器


- 新建一个定时器
```objc
/** 定时器 */
@property (nonatomic,strong) NSTimer *timer
```
- 添加startTimer方法在控件初始化时及scrollview结束滚动时调用 
```objc
/**
 *  开始定时器
 */
-(void)startTimer
{
    self.timer = [NSTimer scheduledTimerWithTimeInterval:1.5 target:self selector:@selector(nextPage) userInfo:nil repeats:YES];
    
    //通知主线程
    [[NSRunLoop mainRunLoop]addTimer:self.timer forMode:NSRunLoopCommonModes];
}
```
- nextPage 控制scrollview的翻页
```objc
/**
 *  下一页
 */
-(void)nextPage
{
    //下一页
    NSInteger page = self.page.currentPage + 1;
    //如果当前页等于最后一页，翻回第一页
    if(page == self.page.numberOfPages){
        page = 0;
    }
    
    CGPoint offset = self.scrollView.contentOffset;
    // 0乘以当前scrollView的contentOffset的x即为第一页
    // 1乘以当前scrollView的contentOffset的x即为第二页
    // ...
    // contentOffset的Y不变
    offset.x = page * self.scrollView.frame.size.width;
    [self.scrollView setContentOffset:offset animated:YES];
    
    NSLog(@"nextPage");
}
```
- 实现`scrollview的scrollViewDidScroll`和`scrollViewWillBeginDragging`协议在开始滚动及结束滚动时控制定时器。
```objc
/**
 *  scrollview开始滚动
 *
 *  @param scrollView
 */
-(void)scrollViewWillBeginDragging:(UIScrollView *)scrollView
{
    [self stopTime];
}
/**
 *  scrollview结束滚动
 *
 *  @param scrollView
 *  @param decelerate
 */
-(void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate
{
    [self startTime];
}
/**
 *  结束定时器
 */
-(void)stopTime
{
    [self.timer invalidate];//停止定时器
    self.timer = nil;
}
```

###最终效果
![滚动](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-6/15652186.jpg)