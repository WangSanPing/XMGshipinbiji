# 三种用代码实现Autolayout的方法


## 第一种 - iOS源生
- 创建约束

```objc

/**
 *  <#Description#>
 *
 *  @param view1      要约束的控件
 *  @param attr1      约束的类型
 *  @param relation   与参照控件之间的关系
 *  @param view2      参照的控件
 *  @param attr2      约束的类型
 *  @param multiplier 乘数
 *  @param c          常量
 *
 *  @return <#return value description#>
 */
+(id)constraintWithItem:(id)view1
attribute:(NSLayoutAttribute)attr1
relatedBy:(NSLayoutRelation)relation
toItem:(id)view2
attribute:(NSLayoutAttribute)attr2
multiplier:(CGFloat)multiplier
constant:(CGFloat)c;
```

- 添加约束

```objc
- (void)addConstraint:(NSLayoutConstraint *)constraint;
- (void)addConstraints:(NSArray *)constraints;
```

- 注意
  - 一定要在拥有父控件之后再添加约束
  - 关闭Autoresizing功能
  
  ```objc
    view.translatesAutoresizingMaskIntoConstraints = NO;
    ```

## 第二种 - VFL

- 使用VFL创建约束数组
  
```objc
+ (NSArray *)constraintsWithVisualFormat:(NSString *)format
options:(NSLayoutFormatOptions)opts
metrics:(NSDictionary *)metrics
views:(NSDictionary *)views;
* format ：VFL语句
* opts ：约束类型
* metrics ：VFL语句中用到的具体数值
* views ：VFL语句中用到的控件
```

- 使用下面的宏来自动生成views和metrics参数

```objc
NSDictionaryOfVariableBindings(...)
```

## 第三种 - 第三方框架 Masonry

- 使用步骤
  -  添加Masonry文件夹的所有源代码到项目中
  -  添加两个宏、导入主头文件

  ```objc
  // 只要添加了这个宏，就不用带mas_前缀
  #define MAS_SHORTHAND
  // 只要添加了这个宏，equalTo就等价于mas_equalTo
  #define MAS_SHORTHAND_GLOBALS
  // 这个头文件一定要放在上面两个宏的后面
  #import "Masonry.h"
  ```
  
- 添加约束的方法

  ```objc
  // 这个方法只会添加新的约束
   [view makeConstraints:^(MASConstraintMaker *make) {
   }];

  // 这个方法会将以前的所有约束删掉，添加新的约束
   [view remakeConstraints:^(MASConstraintMaker *make) {
   }];

   // 这个方法将会覆盖以前的某些特定的约束
   [view updateConstraints:^(MASConstraintMaker *make) {
   }];
  ```

- 约束的类型

  ```objc
  1.尺寸：width\height\size
  2.边界：left\leading\right\trailing\top\bottom
  3.中心点：center\centerX\centerY
  4.边界：edges
  ```





















