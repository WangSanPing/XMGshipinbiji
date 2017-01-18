### 发送同步请求

```objc
+ (NSData *)sendSynchronousRequest:(NSURLRequest *)request returningResponse:(NSURLResponse **)response error:(NSError **)error;
// 这个方法是阻塞式的，会在当前线程发送请求
// 当服务器的数据完全返回时，这个方法才会返回，代码才会继续往下执行
```

### 发送异步请求-block

```objc
+ (void)sendAsynchronousRequest:(NSURLRequest*) request
                          queue:(NSOperationQueue*) queue
              completionHandler:(void (^)(NSURLResponse* response, NSData* data, NSError* connectionError)) handler;
// 会自动开启一个子线程去发送请求
// 当请求完毕（成功\失败），会自动调用handler这个block
// handler这个block会放到queue这个队列中执行
```

### 发送异步请求-delegate
- 创建NSURLConnection对象

```objc
// startImmediately==YES，创建完毕后，自动发送异步请求
- (instancetype)initWithRequest:(NSURLRequest *)request delegate:(id)delegate startImmediately:(BOOL)startImmediately;
- (instancetype)initWithRequest:(NSURLRequest *)request delegate:(id)delegate; // 创建完毕后，自动发送异步请求
+ (NSURLConnection*)connectionWithRequest:(NSURLRequest *)request delegate:(id)delegate; // 创建完毕后，自动发送异步请求
```

- 发送请求

```objc
[connection start];
```

- 遵守`NSURLConnectionDataDelegate`协议，实现协议中的代理方法

```objc
// 当接收到服务器的响应时就会调用
- (void)connection:(NSURLConnection *)connection didReceiveResponse:(NSURLResponse *)response;

// 每当接收到服务器返回的数据时就会调用1次（数据量大的时候，这个方法就会被调用多次）
- (void)connection:(NSURLConnection *)connection didReceiveData:(NSData *)data;

// 当服务器的数据完全返回时调用（服务器的数据接收完毕）
- (void)connectionDidFinishLoading:(NSURLConnection *)connection;

// 当请求失败的时候调用
- (void)connection:(NSURLConnection *)connection didFailWithError:(NSError *)error;
```

- 取消请求

```objc
[connection cancel];
```

## NSString和NSData的互相转换
- NSString -> NSData

```objc
NSData *data = [@"520it.com" dataUsingEncoding:NSUTF8StringEncoding];
```

- NSData -> NSString

```objc
NSString *string = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
```



```objc
  //发送请求给服务器，加载右侧的数据
        NSMutableDictionary *params = [NSMutableDictionary dictionary];
        params[@"a"] = @"list";
        params[@"c"] = @"subscribe";
        params[@"category_id"] =@(c.id);
        [[AFHTTPSessionManager manager] GET:@"http://api.budejie.com/api/api_open.php" parameters:params success:^(NSURLSessionDataTask *task, id responseObject) {
            //字典转模型数组
           NSArray *users = [XJQRecommendUser objectArrayWithKeyValuesArray:responseObject[@"list"]];

            //添加当前类别对应的用户组
            [c.users addObjectsFromArray:users];
            //刷新表格
            [self.detailVC reloadData];

        } failure:^(NSURLSessionDataTask *task, NSError *error) {
            [SVProgressHUD showErrorWithStatus:@"加载数据失败"];
        }];

```
