# UITableView(四)几种常用设置

- #### UITableView的常见设置
  - 设置分割线颜色
  
  ```objc
  self.tableView.separatorColor = [UIColor redColor];
  ```
  
  - 隐藏分割线,在需要自定义分割线时可以先更改该属性，然后再添加想要的分割线样式，用AutoLayout设置在每行的底部即可

  ```objc
  self.tableView.separatorStyle = UITableViewCellSeparatorStyleNone;
  ```
  
- #### UITableViewCell的常见设置
  - 取消选中的样式,在单纯的展示数据时可用
  
  ```objc
  cell.selectionStyle = UITableViewCellSelectionStyleNone;
  ```
  
   - 设置选中的背景色
  
  ```objc
    UIView *selectedBackgroundView = [[UIView alloc] init];
    selectedBackgroundView.backgroundColor = [UIColor redColor];
    cell.selectedBackgroundView = selectedBackgroundView;
  ```
  
   - 设置默认的背景色,两种方法，需要注意的是backgroundView的优先级 大于 backgroundColor
  
    1.
  ```objc
    UIView *selectedBackgroundView = [[UIView alloc] init];
    selectedBackgroundView.backgroundColor = [UIColor redColor];
    cell.selectedBackgroundView = selectedBackgroundView;
  ```

    2.
  ```objc
     cell.backgroundColor = [UIColor blueColor];
  ```
  
  - 设置指示器

    ```objc
    cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
    ```
    
 - 最右侧添加控件

    ```objc
    cell.accessoryView = [[UISwitch alloc] init];
    ```