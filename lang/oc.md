#OC
//设置磁盘缓存
当缓存设置小于200M时，大于500的文件请求时不会携带ETag(If-None-Match,If-Modified-Since)
```
NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:0 diskCapacity:200 * 1024 * 1024 diskPath:nil];
[NSURLCache setSharedURLCache:URLCache];
```