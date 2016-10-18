# UITableView(一)

- ##UITableView简单使用步骤
  1. 设置数据源`dataSource`
  ```objc
  // 设置数据源
  self.tableView.dataSource = self;
  ```
  2. 实现`<UITableViewDataSource>`协议
  3. 实现`<UITableViewDataSource>`协议中的`- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section`和`- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath`方法

```objc

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
    return 2;// 两条
}


/**
 *  每行如何显示
 *
 *  @param tableView tableView
 *  @param indexPath 行号
 *
 *  @return 每行的内容
 */
-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    UITableViewCell *cell = [[UITableViewCell alloc]init];
        // initWithStyle:UITableViewCellStyleSubtitle 显示子标题
//    UITableViewCell *cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleSubtitle reuseIdentifier:nil];
    cell.textLabel.text = @"我是第一组";
    cell.imageView.image = [UIImage imageNamed:@"m_10_100"];//添加图片
    
    if(indexPath.section == 1)
    {
        cell.textLabel.text = @"我是第二组";
        cell.imageView.image = [UIImage imageNamed:@"m_13_100"];
    }
    
    if(indexPath.section == 2)
    {
        cell.textLabel.text = @"我是第三组";
        cell.imageView.image = [UIImage imageNamed:@"m_14_100"];
    }
    
    return  cell;
}

```
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-21/67457894.jpg)
- ##分组的UITableView
  - 把UITableView的style属性改为Grouped
  - 实现`-(NSInteger)numberOfSectionsInTableView:(UITableView *)tableView`方法
 
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
      return 3;// 两组
  }
  ```
  ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-21/85407458.jpg)
- ##给UITableView添加头尾描述部分
  - 实现`-(NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section
`和`-(NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section
`方法
  
  ```objc
    -(NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section
    {
        return @"我是头";
    }

    -(NSString *)tableView:(UITableView *)tableView titleForFooterInSection:(NSInteger)section
    {
        return  @"我是尾";
    }
  ```
  ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-21/86275224.jpg)