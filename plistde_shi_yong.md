# plist的使用

- ##### plist文件是一种资源文件，全名Property List，属性列表文件，它是一种用来存储串行化后的对象的文件。属性列表文件的扩展名为.plist ，因此通常被称为 plist文件。文件是xml格式的。
- ##### plist文件的读取
  - 利用NSBundle对象，一个NSBundle对象对应一个资源包（图片、音频、视频、plis等文件）
  - NSBundle的作用：用来访问与之对应的资源包内部的文件，可以用来获得文件的全路径
  - 项目中添加的资源都会被添加到主资源包中
- #####代码如下
```objc
    // [NSBundle mainBundle] 关联的就是项目的主资源包
    NSBundle *bundle = [NSBundle mainBundle];
    // 利用mainBundle 获得plist文件在主资源包中的全路径
    NSString *file = [bundle pathForResource:@"shops" ofType:@"plist"];
    // 凡是参数名为File，传递的都是文件的全路径
    self.shops = [NSArray arrayWithContentsOfFile:file];
```

- #####懒加载
懒加载的含义：用到时再去加载，而且只加载一次
  - 使用方法: 把数据读取放到shops的get方法中。

```objc
-(NSArray *)shops
{
    if(_shops == nil)
    {
        // 一个NSBundle对象对应一个资源包（图片、音频、视频、plis等文件）
        // NSBundle的作用：用来访问与之对应的资源包内部的文件，可以用来获得文件的全路径
        // 项目中添加的资源都会被添加到主资源包中
        // [NSBundle mainBundle] 关联的就是项目的主资源包
        // 利用mainBundle 获得plist文件在主资源包中的全路径
        NSString *file = [[NSBundle mainBundle] pathForResource:@"shops" ofType:@"plist"];
        // 凡是参数名为File，传递的都是文件的全路径
        self.shops = [NSArray arrayWithContentsOfFile:file];
    }
    return _shops;
}
```

- #####点语法回顾

`@property shops`会自动生成如下代码
```objc
@interface ViewController ()
{
    NSArray *_shops;
}
/**
 *  set方法
 */
-(void)setShops:(NSArray *)shops;
/**
 *  get方法
 */
-(NSArray *)shops;

/**
 *  shops-Set
 */
-(void)setShops:(NSArray *)shops
{
    _shops = shops;
}

/**
 *  shops-Get
 */
-(NSArray *)shops
{
    return _shops;
}
```

```objc
self.shops = nil //等价于[self setShops];
Array *test = self.shops //等价于Array *test = [self shops];
```
