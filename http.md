## Http请求的常见方法
- Get
   - 所有参数拼接在URL后面，并且参数之间用&隔开
    - 比如http://www.baidu.com?name=123&pwd=345
    - 传递了两个参数给服务器
        - name参数：123
        - pwd参数：345
    - 一般用来查询数据
- POST 
    - 所有参数都放在`请求体`中
    - 一般用来修改、增加、删除数据

## 创建HTTP请求

- Get

```objc

NSString *urlString = @"http://520it.com?name=张三&pwd=123";urlString = [urlString stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];

// 创建URLNSURL *url = [NSURL URLWithString:urlString];

// 创建请求NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];

// 设置请求方法（默认就是GET请求）request.HTTPMethod = @"GET";

```

- POST

```objc
// 请求路径NSString *urlString = @"http://520it.com/图片";urlString = [urlString stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];

// 创建URLNSURL *url = [NSURL URLWithString:urlString];

// 创建请求NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];

// 设置请求方法request.HTTPMethod = @"POST";

// 设置请求体request.HTTPBody = [@"name=张三&pwd=123" dataUsingEncoding:NSUTF8StringEncoding];
```
