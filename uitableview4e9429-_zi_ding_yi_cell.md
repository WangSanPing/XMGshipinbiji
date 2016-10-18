# UITableView(五)-自定义Cell(等高及非等高)

- ###等高的自定义Cell
  - ####通过storyboard创建步骤
    - 1.storyboard部分
      - 在storyboard中添加需要的子控件
    ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-25/20616568.jpg)
      - 设置cell的Identifier，以供创建cell时使用
      - 新建类并继承UITableViewCell类
      - 修改cell的class为刚刚新建的类
      - 在类中新建model属性
    - 2.控制器部分
      - 利用cell的Identifier标识找到cell
      - 给cell的模型属性赋值
    - 3.扩展类部分
      - 将storyboard中的子控件连线到扩展类中
      - 需要提供一个模型属性，重写模型的set方法，在这个方法中设置模型数据到子控件上
 
  - ####通过Xib创建步骤
    - 1.Xib部分
      - 同storyboard一样，只是把子控件加入到xib中
    - 2.控制器部分
      - 大体同storyboard，只不过创建cell的方法应改成通过xib文件创建
      - 代码片段
      
      ```objc
    static NSString *idCell = @"first";
    TableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:idCell];
    if(cell == nil){
        cell = [[[NSBundle mainBundle]loadNibNamed:@"UITableCellXib" owner:nil options:nil]lastObject];
    }
      ```
    - 3.扩展类部分
      - 同storyboard。
    - 4.细节优化
      - 在扩展类中新建初始化方法，把创建cell的代码放到该初始化方法中
      - 代码片段
      
      ```objc
      
      +(instancetype)cellWithTable:(UITableView *)tableView
{
    static NSString *idCell = @"first";
    WXTableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:idCell];
    if(cell == nil){
        cell = [[[NSBundle mainBundle]loadNibNamed:@"UITableCellXib" owner:nil options:nil]lastObject];
    }
    return cell;
}
      ```
   - 5 还可以通过注册的方式直接创建一个cell，这样在新建cell时就不用判断cell是否为空
     - 代码片段
     
     ```objc
    UINib *nib = [UINib nibWithNibName:@"UITableCellXib" bundle:nil];
    [self.tableView registerNib:nib forCellReuseIdentifier:@"first"];
     ```


- ###非等高的自定义Cell
  - xib方式
    - 控件布局及数据绑定方式参考等高的自定义Cell
    - 不同点如下
      - 1.在模型中增加一个属性用来存放对应Cell的高度
      - 2.`在Cell的模型属性set方法中调用[self layoutIfNeed]方法强制布局`，不调用该方法得到的Cell高度无法预估。
      - 3.在控制器中实现`-(CGFloat)tableView:(UITableView *)tableView estimatedHeightForRowAtIndexPath:(NSIndexPath *)indexPath`方法，返回一个预估高度，只要返回了估计高度，那么就会先调用`tableView:cellForRowAtIndexPath:`方法创建cell，再调用`tableView:heightForRowAtIndexPath:`方法获取cell的真实高度
      - 4.建议在扩展Cell中实现`awakeFromNib`方法，设置内容label的`preferredMaxLayoutWidth`属性，以避免在Autolayout中计算高度出现偏差。
      
        ```objc
        -(void)awakeFromNib
  {
      self.contentLabel.preferredMaxLayoutWidth = [UIScreen mainScreen].bounds.size.width - 20;
  }
        ```