浏览器缓存分为：强缓存 和 协商缓存 [https://www.jianshu.com/p/54cc04190252](https://www.jianshu.com/p/54cc04190252)

```
强缓存
相关的header
1、Expires: 过期时间 GMT
2、Cache-Control 
max-age = 300s
public 所有内容都将被缓存
private 所有内容只有客户端可以被缓存
no-cache 协商缓存标志 使用Etag 和 Last-Modified 控制缓存
no-store 不使用任何缓存
max-age 缓存在多少s后失效
协商缓存
1、last-modified 和 if-modified-since 文件无更新 则返回 304 有更新返回200
缺点：
服务器不能获取精确时间，秒为单位 1s内发生变化无感知 
时间变更，但是实际内容不变
2、使用Etag 和 if-none-match 客户端 304返回

用户缓存的机制
1、地址栏访问，链接跳转是正常用户行为，将会触发浏览器缓存机制；
2、F5刷新，浏览器会设置max-age=0，跳过强缓存判断，会进行协商缓存判断；
3、ctrl+F5刷新，跳过强缓存和协商缓存，直接从服务器拉取资源。

```

CDN缓存

