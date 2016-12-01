## JSON数据和OC对象互转

#### JSON数据 (NSData)  -> OC对象(Foundation Object)

- {} -> NSDictionary @{}
- [ ] -> NSArray @[ ]
- "jack" -> NSString @"jack"
- 10 -> NSNumber @10
- 10.5 -> NSNumber @10.5
- true -> NSNumber @1
- false -> NSNumber @0
- null -> NSNull

#### JSON数据(NSData)  -> OC对象(Foundation Object)

```objc

// 利用NSJSONSerialization类
+ (id)JSONObjectWithData:(NSData *)data options:(NSJSONReadingOptions)opt error:(NSError **)error;

```