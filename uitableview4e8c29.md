# UITableView(二)结合Model加载数据

把UITableView中的每个分组都看成一个整体，每一行都看成组中的单个数据。

故需要建立两个Model
  - ###CarGroup`(GroupModel)` 代表每个分组，用来存放行数据
 
 ```objc
 
  @interface CarGroup : NSObject

  /** 头 */
  @property (nonatomic,strong) NSString *head;

  /** 尾 */
  @property (nonatomic,strong) NSString *foot;

  /** 汽车 */
  @property (nonatomic,strong) NSArray *cars;

  @end

 ```
 
  - ###Car`(DataModel)` 代表每行。
  
  ```objc
  
  @interface Car : NSObject

  /** 汽车名称 */
  @property (nonatomic,strong) NSString *carName;

  /** 图片 */
  @property (nonatomic,strong) NSString *imageName;

  /**
   *  初始化
   *
   *  @param carName   汽车名称
   *  @param imageName 图片名称
   *
   *  @return 返回带汽车名称和图片名称的Car类
   */
  +(instancetype)initWithData:(NSString *)carName imageName:(NSString *)imageName;

  @end

  #import "Car.h"

  @implementation Car

  +(instancetype)initWithData:(NSString *)carName imageName:(NSString *)imageName
  {
      Car *car = [[Car alloc]init];
      car.carName = carName;
      car.imageName = imageName;
      return car;
  }

  @end

  ```
  
- ###接下来修改原有代码，新建一个数据用来存放每组CarGroup。
  
  ```objc
  /** 组数据 */
@property (nonatomic,strong) NSArray *groups;
  ```
  
-  ###采用懒加载的方式加载数据.
  
  ```objc
  -(NSArray *)groups
{
    /**
     *  用到时再赋值，并且只赋值一次
     */
    if(_groups == nil)
    {
        CarGroup *group = [[CarGroup alloc]init];
        group.head = @"我是头111111";
        group.foot = @"我是尾111111";
        group.cars = @[[Car initWithData:@"丰田111" imageName:@"m_2_100"],
                       [Car initWithData:@"路虎111" imageName:@"m_2_100"],
                       [Car initWithData:@"马自达111" imageName:@"m_2_100"],
                       [Car initWithData:@"三菱111" imageName:@"m_2_100"]];
        
        CarGroup *group1 = [[CarGroup alloc]init];
        group1.head = @"我是头222222";
        group1.foot = @"我是尾222222";
        group1.cars = @[[Car initWithData:@"丰田222" imageName:@"m_3_100"],
                        [Car initWithData:@"路虎222" imageName:@"m_3_100"],
                        [Car initWithData:@"马自达222" imageName:@"m_3_100"]];
        
        _groups = @[group,group1];
    }
    
    return _groups;
}
  
  ```

- 下面代码为整体修改后的代码，需要说明的是`UITableViewDataSource`协议中的每个方法的`section`代表分组的序号，`-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
`方法中的indexPath存有当前组和当前行的序号


 ```objc
    /**
     *  分组
     *
     *  @param tableView tableView
     *
     *  @return 返回几组
     */
    -(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView
    {
        return self.groups.count;// 两组
    }


    /**
     *  标记多少行数据
     *
     *  @param tableView tableView
     *  @param section   组号
     *
     *  @return 返回行数
     */
    -(NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
    {
        CarGroup *group =self.groups[section];
        return group.cars.count;// 两条
    }


    /**
     *  每行如何显示
     *
     *  @param tableView tableView
     *  @param indexPath
     *
     *  @return 每行的内容
     */
    -(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
    {
        UITableViewCell *cell = [[UITableViewCell alloc]init];
        // 取出分组
        CarGroup *group = self.groups[indexPath.section];
        // 在分组中取出每个Car的数据
        Car *car = group.cars[indexPath.row];
        cell.textLabel.text = car.carName;
        cell.imageView.image = [UIImage imageNamed:car.imageName];

        // initWithStyle:UITableViewCellStyleSubtitle 显示子标题
        //    UITableViewCell *cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:nil];
        //    cell.textLabel.text = @"我是第一组";
        //    cell.imageView.image = [UIImage imageNamed:@"m_10_100"];
        //
        //    if(indexPath.section == 1)
        //    {
        //        cell.textLabel.text = @"我是第二组";
        //        cell.imageView.image = [UIImage imageNamed:@"m_13_100"];
        //    }
        //
        //    if(indexPath.section == 2)
        //    {
        //        cell.textLabel.text = @"我是第三组";
        //        cell.imageView.image = [UIImage imageNamed:@"m_14_100"];
        //    }
        //
        return  cell;
    }

    /**
     *  头
     */
    -(NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section
    {
        CarGroup *gruop = self.groups[section];

        return gruop.head;
    }

    /**
     *  尾
     */
    -(NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section
    {
        CarGroup *gruop = self.groups[section];

        return gruop.foot;
    }

```

## 效果

![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-22/23066710.jpg)