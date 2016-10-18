# UITableView(三)简单性能优化

####iOS的UITableView在数据加载时采用的是懒加载的方式，也就是说每行数据是只有在用到时才会加载。
  - 通过观察下图UITableView在滑动时调用`-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
`的时机就可判断出UITableView采用的是懒加载方式
![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-23/50185101.jpg)

####虽然iOS已经为UITableView采用了懒加载方式加载数据，但是频繁的创建及销毁对象对性能还是有一定影响，因此iOS还提供了另一种加载方式 - 通过缓存池加载。
 - 思路
   - UITableView在每次加载行数据时都会把已经不在当前显示的行放入到一个缓存池中
   - 故在每次加载新的行数据时可以先到缓存池中查找当前是否有可用的cell，有的话就拿出来重新赋值。这样就可以避免频繁的创建及销毁对象。
     - 需要注意：即在创建cell时需要给个标识，这样才能准确的拿出来当前UITableview可使用的cell
   - 代码片段如下
   
   ```objc
   -(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    // 从缓存池中查找标示为test的cell
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"test"];
    
    // 判断在缓存池中是否存在
    if(cell == nil)
    {
        // 在创建cell时就为该cell标示为test
        cell = [[UITableViewCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"test"];
    }
    
    cell.textLabel.text = [NSString stringWithFormat:@"data----%zd",indexPath.row];
    NSLog(@"%p----%zd",cell,indexPath.row);
    
    return  cell;
}
   ```
 ![](http://7xrpl5.com1.z0.glb.clouddn.com/16-4-23/52061386.jpg)
 
####通过观察上图,可以看到前四行和8、9、10、11行的内存地址是一样的。也就是说是在缓存池中取出来的。这样就减少了频繁的创建、销毁对象，也就起到了优化性能的目的。



