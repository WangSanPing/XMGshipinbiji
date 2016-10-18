# UIApplication

* ###整个app中只有一个UIApplication，是单例的
* ###UIApplication一般用来做一些应用级别的操作(app的提醒框，联网状态，打电话，打开网页，控制状态栏)
  - 设置app的右上角角标
  
  ```objc
    // UIApplication是单例的，即在内存中只有一格实例化的UIApplication
    UIApplication *app = [UIApplication sharedApplication];
    
    // 设置右上角标数字，必须注册用户通知，否则不生效
    app.applicationIconBadgeNumber = 10;
    
    // 创建用户通知
    UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeBadge categories:nil];
    
    // 注册用户通知
    [app registerUserNotificationSettings:settings];
  ```
  - 设置联网状态
 
  ```objc
    // UIApplication是单例的，即在内存中只有一格实例化的UIApplication
    UIApplication *app = [UIApplication sharedApplication];
    
    app.networkActivityIndicatorVisible = YES;

  ```
  
   - 隐藏状态栏
     - 需要注意的是在iOS7以后Apple建议状态栏默认由控制器决定。如果想要由UIApplication决定需要在info.plist里加一条View controller-based status bar appearance的key并把value设置为NO
   
  ```objc
    // 获取UIApplication
    UIApplication *app = [UIApplication sharedApplication];

    [app setStatusBarHidden:YES withAnimation:UIStatusBarAnimationSlide];
  ```
  
  - 利用openURL方法打开网页、打电话、发短信、打开网页
  
 ```objc
        
    UIApplication *app = [UIApplication sharedApplication];
    
    // 打电话
    [app openURL:[NSURL URLWithString:@"tel://1234567"]];
    
    // 发短信
    [app openURL:[NSURL URLWithString:@"sms://1234567"]];
    
    // 发邮件
    [app openURL:[NSURL URLWithString:@"mailto://12345@qq.com"]];
    
    // 打开网页
    [app openURL:[NSURL URLWithString:@"http://www.baidu.com"]];
  ```

- ###UIApplication的系统默认创建的delegate方法

```objc
  // 程序启动完成的时候调用
  - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
      // Override point for customization after application launch.
      NSLog(@"%s",__func__);
      return YES;
  }

  // 当app失去焦点的时候调用
  - (void)applicationWillResignActive:(UIApplication *)application {
          NSLog(@"%s",__func__);
      // Sent when the application is about to move from active to inactive state. This can occur for certain types of temporary interruptions (such as an incoming phone call or SMS message) or when the user quits the application and it begins the transition to the background state.
      // Use this method to pause ongoing tasks, disable timers, and throttle down OpenGL ES frame rates. Games should use this method to pause the game.
  }

  // app进入后台的时候调用
  // app忽然打断的时候，在这里保存一些需要用到的数据
  - (void)applicationDidEnterBackground:(UIApplication *)application {
          NSLog(@"%s",__func__);
      // Use this method to release shared resources, save user data, invalidate timers, and store enough application state information to restore your application to its current state in case it is terminated later.
      // If your application supports background execution, this method is called instead of applicationWillTerminate: when the user quits.
  }


  // app进入即将前台
  - (void)applicationWillEnterForeground:(UIApplication *)application {
          NSLog(@"%s",__func__);
      // Called as part of the transition from the background to the inactive state; here you can undo many of the changes made on entering the background.
  }

  // 当app获取到焦点的时候调用，意味着app可以与用户交互
  - (void)applicationDidBecomeActive:(UIApplication *)application {
          NSLog(@"%s",__func__);
      // Restart any tasks that were paused (or not yet started) while the application was inactive. If the application was previously in the background, optionally refresh the user interface.
  }

  // app被关闭的时候调用
  - (void)applicationWillTerminate:(UIApplication *)application {
          NSLog(@"%s",__func__);
      // Called when the application is about to terminate. Save data if appropriate. See also applicationDidEnterBackground:.
  }


  // app接收到内存警告的时候调用
  // 清空图片的缓存
  - (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
  {
      NSLog(@"%s",__func__);
  }

  ```
  