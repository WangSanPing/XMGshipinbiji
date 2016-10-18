# 简单动画介绍

- 在程序中使用动画的几种方法
  - 直接创建动画

  ```objc
  // 动画开始
  [UIView beginAnimations:nil context:nil];
  // 设置延迟时间
  [UIView setAnimationDuration:1];
  // 设置委托
  [UIView setAnimationDelegate:self];
  // 动画结束后执行
  [UIView setAnimationDidStopSelector:@selector(stop)];
  // 动画开始前执行
  [UIView setAnimationWillStartSelector:@selector(start)];
  CGFloat y = self.image.frame.size.height - self.scrollView.frame.size.height;
  self.scrollView.contentOffset = CGPointMake(self.scrollView.contentOffset.x, y);
  // 提交动画，否则没有动画
  [UIView commitAnimations];
  ```
  - 类方法

  ```objc
  CGPoint offset = CGPointMake(self.scrollView.contentOffset.x, 0);
  [self.scrollView setContentOffset:offset animated:YES];
  ```
  
  - block
  
  ```objc
  [UIView animateWithDuration:1 animations:^{
          self.scrollView.contentOffset = CGPointMake(0, self.scrollView.contentOffset.y);
      } completion:^(BOOL finished){
          if(finished)
          {
               NSLog(@"执行完毕");
          }
      }];
  ```