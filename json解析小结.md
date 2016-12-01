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


- 利用NSJSONSerialization类

```objc

 /**

 NSJSONReadingOptions 说明


 NSJSONReadingMutableContainers = (1UL << 0) 创建出来的数据和字典是可变的

 NSJSONReadingMutableLeaves = (1UL << 1) 数组或者字典里面的字符串是可变的

 NSJSONReadingAllowFragments 允许解析出来的对象不是字典或者数组，比如直接是字符串或者NSNumber

 */

 + (id)JSONObjectWithData:(NSData *)data options:(NSJSONReadingOptions)opt error:(NSError **)error;


```
- 

    
    