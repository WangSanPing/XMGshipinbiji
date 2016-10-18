# 使用tableHeaderView和tableFooterView实现头广告轮播及尾部加载更多数据

## 先看下效果
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-19/69389188.jpg)



  实现这两个需求很简单，因为TableView的tableHeaderView和tableFooterView这两个属性都是UIView类型的，我们只需要给TableView的tableHeaderView和tableFooterView赋值两个UIView类型就可以了。
  - ##tableHeaderView
    - 对于头部tableHeaderView的实现需要用到之前介绍的图片轮播demo( [ScrollView实现图片轮播及封装自定义控件](http://www.jianshu.com/p/906f838fa25f))
    - 把该项目中的实现文件直接拖入到现有的项目中
    - 针对于之前的轮播控件封装，我们只需要在调用时给该控件的imageNames赋值即可。
    
      ```objc
      WXPageView *pageView = [WXPageView PageView];
      pageView.imageNames = @[@"2c97690e72365e38e3e2a95b934b8dd2",
                              @"5ee372ff039073317a49af5442748071",
                              @"9b437cdfb3e3b542b5917ce2e9a74890",
                              @"37e4761e6ecf56a2d78685df7157f097",
                              @"2010e3a0c7f88c3f5f5803bf66addd93",
                              @"53453be0d2dd458c057286d17f6b9306"];

      // 头
      self.tableView.tableHeaderView = pageView;

      ```
      
  - ##tableFooterView
    - tableFooterView和tableHeaderView的实现思路是一样的，只是为了实现点击加载更多这个需求我们还需要对该需求进行说明
    - 实现思路
      - 通过xib文件进行布局，其中内容如下图。
      ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-19/3904875.jpg)
      注意红框部分，里面还包含一个UIView，这个UIView里面包含loading展示的界面。
      - 当点击加载更多时把LoadMoreButton设为隐藏，正在加载更多设为展示。
        - 关键点为tableView的controller和子控件的交互。这里用的是通知的方式。
        
        在tableView的controller中监听通知
        ```objc
        // 在tableView的controller中监听通知
        [[NSNotificationCenter defaultCenter]addObserver:self selector:@selector(loadMoreDeals) name:@"loadMore" object:nil];
        
        /**
         *  一定要在dealloc中移除通知！一定要在dealloc中移除通知！一定要在dealloc中移除通知！
         */
        - (void)dealloc{
            [[NSNotificationCenter defaultCenter] removeObserver:self];
        }
        ```
        在子控件的点击加载更多按钮的响应事件中发送通知
        ```objc
        - (IBAction)loadMore:(id)sender {
          self.loadMoreButton.hidden = YES;
          self.loadingMoreView.hidden = NO;
          // 发送通知
          [[NSNotificationCenter defaultCenter] postNotificationName:@"loadMore" object:nil];
      }
        ```
        
 [源码下载](https://github.com/WangSanPing/-tableHeaderView-tableFooterView-)