# Xib文件的使用

- Xib文件也是一种描述控件布局的文件
- Xib和storyboard的对比
  - 共同点
    - 都用来描述软件界面
    - 都用interface builder工具来编辑
    - 本质都是转换成代码去创建控件

  - 不同点
    - Xib是轻量级的，用来描述局部的UI界面
    - Storyboard是重量级的，用来描述整个软件的多个界面，并且能展示多个界面之间的跳转关系
 
- Xib的加载方法 
  ```objc
    //第一种
    NSArray *views = [[NSBundle mainBundle] loadNibNamed:@"xib文件名" owner:nil options:nil]
    //第二种
    UINib *nib = [UINib nibWithNibName:@"xib文件名" bundle:nil];
    NSArray *views = [nib instantiateWithOwner:nil options:nil];
  ```

- 注意点
  - 通过xib\storyboard创建
    - 初始化时不会调用initWithFrame：方法，只会调用initWithCoder：方法
    - 初始化完毕后会调用awakeFromNib方法
    - 有时候希望在控件初始化时做一些初始化操作，比如添加子控件、设置基本属性，这时需要根据控件的创建方式，来选择在initWithFrame:、initWithCoder:、awakeFromNib的哪个方法中操作
