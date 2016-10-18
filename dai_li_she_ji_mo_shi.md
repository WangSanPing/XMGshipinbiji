  在[使用tableHeaderView和tableFooterView实现头广告轮播及尾部加载更多数据](http://www.jianshu.com/p/6948957a9863)中我们是使用通知的方式来使Controller类和子控件进行交互的。这种方式对于封装来讲不是很好，因为在Controller类中还需要知道子控件发出通知的key以便监听子控件发出的通知，如果不看子控件的源码是无法知道的。所以这篇使用代理设计模式来实现交互。
# 代理设计模式简介
- 代理设计模式的作用
  - A对象监听B对象的一些行为，A成为B的代理
  - B对象想告诉A对象一些事情，A成为B的代理 
- 代理设计模式的总结
  - 如果你想监听别人的一些行为，那么你就要成为别人的代理
  - 如果你想告诉别人一些事情，那么就让别人成为你的代理
- 代理设计模式的实现步骤
  - 1.制定协议(协议名字的格式：控件名+Delegate),在协议里面声明一些代理方法（一般代理方法都是@optional（非必须实现的））
    ```objc
    /**
     *  WXLoadMoreFooterDelegate
     */
    @protocol WXLoadMoreFooterDelegate <NSObject>

    @optional
    /**
     *  加载更多按钮点击后发生
     */
    -(void)loadMoreFooterDidClickLoadMoreButton:(WXLoadMoreFooter *)footer;
    @end
    ```
  - 2.声明一个代理属性：@property(nonatomic,weak) id<代理协议> delegate；
    - 注意要使用weak，避免强引用循环
    
    ```objc
    /** delegate */
    @property (nonatomic,weak) id<WXLoadMoreFooterDelegate> delegate;
    ```
  - 3.在内部发生某些行为时，调用代理对应的代理方法，通知代理内部发生什么事情
    ```objc
    - (IBAction)loadMore:(id)sender {
    self.loadMoreButton.hidden = YES;
    self.loadingMoreView.hidden = NO;
    
      //注意判断代理实现类是否实现了方法
      if([self.delegate respondsToSelector:@selector(loadMoreFooterDidClickLoadMoreButton:)])
      {
          [self.delegate loadMoreFooterDidClickLoadMoreButton:self];
      }
    }
    ```
  - 4.设置代理: xxx.delegate = yyy;
  ```objc
    WXLoadMoreFooter *footer = [WXLoadMoreFooter LoadMoreFooter];
    footer.delegate = self;
  ```
  - 5.yyy对象遵守协议，实现代理方法。
  ```objc
  
    -(void)loadMoreFooterDidClickLoadMoreButton:(WXLoadMoreFooter *)footer{
        [self loadMoreDeals];
    }

    - (void)loadMoreDeals{
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2.0 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
            WXData *deal = [[WXData alloc]init];

            deal.icon = @"2c97690e72365e38e3e2a95b934b8dd2";
            deal.title = @"xxxx";
            deal.price =[NSString stringWithFormat:@"%d",arc4random_uniform(1000)];
            deal.buyCount = @"90";
            [self.list addObject:deal];

            // 刷新表格
            [self.tableView reloadData];

            WXLoadMoreFooter *footer = (WXLoadMoreFooter *)self.tableView.tableFooterView;
            [footer endLoading];
        });
    }
  ```

# 代理和通知的区别
- 代理：一个对象只能告诉另一个对象发生了什么事
- 通知：一个对象可以告诉N个对象发生了什么事


[源码下载](https://github.com/WangSanPing/delegate_test)