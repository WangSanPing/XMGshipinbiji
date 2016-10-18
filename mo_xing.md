# 模型

- #####什么是模型
  - 专门用来存放数据的对象
  - 一般都是一些直接继承自NSObject的纯对象
  - 内部会提供一些属性来存放数据
- #####用模型取代字典的好处
  - 使用字典的坏处
    - 一般情况下，设置数据和去除数据都使用『字符串类型的key』，编写这些key时，编辑器没有智能提示，需要手动敲写
  ```objc
  dict[@"name"] = @"Jack";
  NSString *name = dict[@"name"];
  ```
    - 手敲字符串key容易写错
    - key如果写错了，编译器不会有任何提示
- ##### 使用模型的好处
  - 所谓模型其实就是数据模型，专门用来存放数据的对象，用它来表示数据会更加专业
  - 模型设置数据和取出数据都是通过它的属性，属性名如果写错了，编译器会马上报错，因此，保证了数据的正确性
  - 使用模型访问属性时，编译器会提供一系列的提示，提高编码效率
  ```objc
  app.name = @"Jack";
  NSString *name = app.name;
  ```
- #####字典转模型
  - 字典转模型的过程最好封装在模型内部
  - 模型应该提供一个可以传入字典参数的构造方法

```objc
  - (instancetype)initWithDict:(NSDictionary *)dict;
  + (instancetype)xxxWithDict:(NSDictionary *)dict;
```

##### instancetype类型
- `instancetype`在类型表示上，跟`id`一样，可以表示任何对象类型
- `instancetype`只能用在返回值类型上，不能像`id`一样用在参数类型上
- `instancetype`比`id`多一个好处：编译器会检测`instancetype`的真实类型，减少出错几率