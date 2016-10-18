# 第一个iOS程序


## storyboard文件的认识
* 是用来描述软件界面的。
* 默认情况下，程序一启动就会加载Main.storyboard
* 更改默认stortboard的方法为选择项目,在General选项卡下找到Main interface，选择其他的storyboard。另需要更改箭头所指的storyboard。

## IBAction 和 IBOutlet
* IBAction:
    - 本质就是void
    - 能让方法具备连线的功能
* IBOutlet:
    - 能让属性具备连线的功能

## storyboard 连线容易出现的问题
- 连接的方法被删掉，但是连线没有去掉
    - 会出现方法找不到的错误
    - 错误信息是----unrecognized selector sent to instance
- 连接的属性被删掉，但是连线没有去掉
    - 会出现属性找不到的错误
    - 错误信息是----this class is not key value coding-compliant for the key label.（其中lable为key，即为storyboard上的控件）。


## UIViewController(控制器)的认识
- 一个控制器负责管理一个大界面
- 控制器负责界面的创建、事件处理等


## 类扩展

- 格式

```objc
@interface 类名()
/** 属性、方法的声明*/
@end
```

- 作用
    - 为某个类增加额外的属性和方法声明
    - 可以写在.h和.m文件中



