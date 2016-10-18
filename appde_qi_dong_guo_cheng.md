# app的启动过程

- main函数为程序入口
  - 在main函数中调用UIApplicationMain方法
    - 通过UIApplicationMain方法创建UIApplication对象
    - 创建UIApplicationDelegate，并且成为UIApplication代理
    - 开启主运行循环，保持程序一直在运行
    - 加载info.plist,判断有没有指定main.stroyboard，如果指定就去加载
      - 创建UIWindow对象
      - 加载main.storyboard,并且加载main.storyboard指定的控制器
      - 把新创建的控制器作为窗口的根控制器，让窗口显示出来
      
      
![思维导图](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-24/16511434.jpg)
      
      
      