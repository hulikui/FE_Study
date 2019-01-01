1. 前端最经典的网络问题：从浏览器输入url后到展示网页发生了什么
   ```js
   越详细越好，
   主要考察http应用层协议相关
   浏览器渲染原理
   以及其他计算机网络知识
   ```
2. http响应头 状态码的解释

   ```js
   1XX－信息类(Information), 表示收到Web浏览器请求，正在进一步的处理中
   2XX-成功类(Successful), 表示用户请求被正确接收，理解和处理例如：200 OK
   3XX-重定向类(Redirection), 表示请求没有成功，客户必须采取进一步的动作。
   4XX-客户端错误(Client Error)，表示客户端提交的请求有错误 例如：404 NOT Found，意味着请求中所引用的文档不存在。
   5XX-服务器错误(Server Error), 表示服务器不能完成对请求的处理：如 500

   对于我们Web开发人员来说掌握HTTP应答码有助于提高Web应用程序调试的效率和准确性。
   301 和 302 
   301 永久重定向，有利于SEO
   302 临时重定向
   ```

3. （备选 加分）高级进阶知识点 HTTP缓存 知识点（查看缓存）

4. TCP/IP协议以及三次握手等等[ https://www.jianshu.com/p/43a25804b2e8](https://www.jianshu.com/p/43a25804b2e8)

5. Http一些重要字段

   ```
   Host 任何情况下，请求都会包含此信息 —— 应用 代理服务器
   客户端标记的我要访问的web服务器的 域名、IP和端口
   Origin
   请求来源，仅仅包括协议和域名，CORS Access-Control-Allow-Origin
   CRSF 验证
   Referer
   发起请求前把window.location.href赋值到referer 向服务器请求的原始资源URI，包括 协议+域名+参数
   用处就是 防盗链
   ```

6. 


