# 指示器

## HUD
- #####其他说法：指示器、遮盖、蒙版
- 半透HUD的做法
  - 背景色设置为半透明颜色

## 定时任务
- #####方法1：performSelector

```objc
// SEL:对方法的包装, 使用@selector(方法名)包装一个SEL数据
// 1.5s以后会自动调用self的hidHUD方法
[self performSelector:@selector(hideHUD) withObject:nil afterDelay:1.5];
```

- #####方法2：GCD

```objc
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(1.5 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
    //1.5s后调用block
        self.Hub.alpha = 0.0;
    });
```

- #####方法3：Timer

```objc
//repeats为no时只调用一次 为YES时重复调用
NSTimer scheduledTimerWithTimeInterval:1.5 target:self selector:@selector(hideHUD) userInfo:nil repeats:NO];
```

## 目前项目效果
![指示器](http://7xrpl5.com1.z0.glb.clouddn.com/16-3-11/56632225.jpg)
