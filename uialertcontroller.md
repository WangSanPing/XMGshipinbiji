# UIAlertController

- ####我在[UITableView(六)数据更新(增、删、改)](http://www.jianshu.com/p/d0e5d0f583cc)中新增方法的数据写的是固定数据，不能自己添加。所以在这篇会用UIAlertController把新增改为自己输入数据的方式。
  - 小tips
    - 苹果在iOS8之后用`UIAlertController`替代了`UIActionSheet`和`UIAlertView`

- #### 修改Add方法如下(请参考《[UITableView(六)数据更新(增、删、改)](http://www.jianshu.com/p/d0e5d0f583cc)》)

```objc

- (IBAction)Add:(UIButton *)sender {
    
    UIAlertController *alert = [UIAlertController alertControllerWithTitle:@"新增" message:nil preferredStyle:UIAlertControllerStyleAlert];
    
    // 添加文本框
    [alert addTextFieldWithConfigurationHandler:^(UITextField *textField) {
        textField.placeholder = @"请输入title";
    }];
    
    [alert addTextFieldWithConfigurationHandler:^(UITextField *textField) {
        textField.placeholder = @"请输入价格";
    }];
    
    // 按钮
    [alert addAction:[UIAlertAction actionWithTitle:@"取消" style:UIAlertActionStyleCancel handler:nil]];
    // 确定按钮
    [alert addAction:[UIAlertAction actionWithTitle:@"确定" style:UIAlertActionStyleDestructive handler:^(UIAlertAction *action){
        WXData *data = [[WXData alloc]init];
        data.title = alert.textFields[0].text;
        data.price = alert.textFields[1].text;
        //        data.buyCount = @"22";
        data.icon = @"2c97690e72365e38e3e2a95b934b8dd2";
        
        // 在数据源的第一个位置插入数据
        [self.list insertObject:data atIndex:0];
        
        // 刷新插入行，有动画效果
        [self.tableView insertRowsAtIndexPaths:@[[NSIndexPath indexPathForRow:0 inSection:0]] withRowAnimation:UITableViewRowAnimationLeft];
    }]];
    
    // 显示控制器
    [self presentViewController:alert animated:YES completion:nil];
    
    
    //    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"111" message:@"2222" delegate:self cancelButtonTitle:@"取消" otherButtonTitles:@"好的", nil];
    //    [alert show];
    
    
    // 刷新全部数据，但是没有动画效果
    // self.tableView reloadData];
}

```

- ####最终效果如下

![](http://7xrpl5.com1.z0.glb.clouddn.com/16-5-3/95612131.jpg)
