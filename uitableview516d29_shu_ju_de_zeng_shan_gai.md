# UITableView(六)数据更新(增、删、改)

- ### 新建一个包含UITableView的View并绑定好测试数据，本文所用的布局如下图
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-1/53763418.jpg)
- ### 分别对添加、编辑、修改、删除四个按钮添加点击事件
  - ####添加按钮的实现代码
    
    ```objc
    
    - (IBAction)Add:(UIButton *)sender {
    WXData *data = [[WXData alloc]init];
    data.price =[NSString stringWithFormat:@"%d",arc4random_uniform(1000)];
    data.title = @"我是新增的";
    data.buyCount = @"22";
    data.icon = @"2c97690e72365e38e3e2a95b934b8dd2";
    
    // 在数据源的第一个位置插入数据
    [self.list insertObject:data atIndex:0];
    
    // 刷新插入行，有动画效果
    [self.tableView insertRowsAtIndexPaths:@[[NSIndexPath indexPathForRow:0 inSection:0]] withRowAnimation:UITableViewRowAnimationLeft];
    
    // 刷新全部数据，但是没有动画效果
    // self.tableView reloadData];
}
    
    ```
    
  - ####编辑按钮的实现代码
  
    ```objc
    - (IBAction)Edit:(UIButton *)sender {
      // 设置tableView是否进入编辑模式
      [self.tableView setEditing:!self.tableView.isEditing animated:YES];
  }
    ```
    
  - ####删除按钮的实现代码
  
    ```objc
    - (IBAction)remove:(UIButton *)sender {
        [self.list removeObjectAtIndex:0]; //从模型中删除

        [self.tableView deleteRowsAtIndexPaths:@[[NSIndexPath indexPathForRow:0 inSection:0]]  withRowAnimation:UITableViewRowAnimationRight];
    }
    ```
    
  - ####更新按钮的实现代码
  
    ```objc
    - (IBAction)Update:(UIButton *)sender {
    WXData *data = self.list[0];
    data.price = [NSString stringWithFormat:@"%d",50 + arc4random_uniform(100)];
    
    [self.tableView reloadData];
}
    ```
    

- ###效果如下

![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-1/17749273.jpg)
    
    
- ###注意点
  - tableView的数据操作全部是通过模型数据来进行的，应该先修改模型数据再调用刷新方法。
  - ###`不要直接修改Cell上面控件的数据。不要直接修改Cell上面控件的数据。不要直接修改Cell上面控件的数据。`


- ###左滑删除效果
  - UITableView的左滑删除方法只需要实现-(void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath 方法，功能实现需要写到该方法中。
  
  ```objc
  
  -(void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath{
    
    if(editingStyle == UITableViewCellEditingStyleDelete){ // 删除
        [self.list removeObjectAtIndex:indexPath.row]; //从模型中删除
        
        [tableView deleteRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationLeft];
    } if(editingStyle == UITableViewCellEditingStyleInsert) // 新增
    {
        NSLog(@"新增");
    }
}

  ```
  
  ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-1/54194460.jpg)
    
    - ###小tips
    可能以后会碰到奇葩需求，需要在编辑状态下需要有新增按钮，apple其实是有提供的。只需要实现- (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath方法即可。
    
    ```objc
    /**
   * 这个方法决定了编辑模式时，每一行的编辑类型：insert（+按钮）、delete（-按钮）
   */
  - (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath
  {
      return indexPath.row % 2 == 0? UITableViewCellEditingStyleInsert : UITableViewCellEditingStyleDelete;
  }

    ```
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    