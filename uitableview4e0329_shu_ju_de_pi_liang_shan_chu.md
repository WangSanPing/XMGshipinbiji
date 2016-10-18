# UITableView(七)数据的批量删除

###前情提要！
 [UITableView(六)数据更新(增、删、改)](http://www.jianshu.com/p/d0e5d0f583cc)

####在开发中对于批量删除这种需求还是挺常见的，本文介绍的实现方式为两种，一种是iOS提供的，另一种为自定义方式。区别是iOS提供的可定制性太差，自定义的可以按需求自己做。

  - ####第一种：利用iOS提供的批量处理数据的方法删除。
    -  1.在`viewDidLoad`方法中设置`tableView`的属性`allowsMultipleSelectionDuringEditing`为YES
    ```objc
     // 允许在编辑模式进行多选操作
     self.tableView.allowsMultipleSelectionDuringEditing = YES;
    ```
    -  2.给编辑按钮添加点击事件，之后实现代码如下
    ```objc
        // 设置tableView是否进入编辑模式
    [self.tableView setEditing:!self.tableView.isEditing animated:YES];
     self.tableView.allowsMultipleSelectionDuringEditing = YES;
    ```
    -  3.给删除按钮添加点击事件，之后实现代码如下
      ```objc
      // 批量删除 - 系统提供
      // 取出所选行
      NSArray *indexPaths = [self.tableView indexPathsForSelectedRows];

      // 存放要删除的数据
      NSMutableArray *delete = [NSMutableArray array];

      // 在原有数据中取出数据
      for (NSIndexPath *item in indexPaths) {
          [delete addObject:self.list[item.row]];
      }

      // 删除数据
      [self.list removeObjectsInArray:delete];

      // 刷新
      [self.tableView reloadData];
      ```
    - 效果
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-4/60815878.jpg)

  - ####第二种：自己实现批量删除。思路为在模型中添加属性标识该行是否被选中，如选中就删除。
    -  1.布局文件中添加一个图片控件用于标识是否被选中。如下图中的绿色对号。
    ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-4/52608817.jpg)
    -  2.把刚添加的图片控件关联到`UITableViewCell`的扩展类中，并在模型类中添加属性标识是否被选中。
    ```objc
    // 对是否选中取反，没有被选中的话就隐藏图片控件,check属性是是否选中标识
    self.check.hidden = !data.IsCheck;
    ```
    -  3.实现UITableView的`didSelectRowAtIndexPath`方法
    ```objc
    -(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath{
        WXData *data = self.list[indexPath.row];
        data.check = !data.IsCheck;
    
        [tableView reloadData];
}
    ```
    -  4.给删除按钮添加点击事件，之后实现代码如下
      ```objc
      // 批量删除 - 自定义

      // 存放要删除的数据
      NSMutableArray *delete = [NSMutableArray array];

      for (WXData *item in self.list) {
          if(item.IsCheck)
          {
              [delete addObject:item];
          }
      }

      // 删除数据
      [self.list removeObjectsInArray:delete];

      // 刷新
      [self.tableView reloadData];
      ```
    - 效果
    
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-4/60815878.jpg)