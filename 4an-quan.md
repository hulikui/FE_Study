1. [浏览器的同源策略](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)（比较重要）

   ```
   解释下定义
   localhost 与 127.0.0.1 算跨域吗？不算
   ```

2. XSS 跨站脚本攻击

   ```js
   原因：1. 浏览器可以拼接任何JavaScript语句
        2. 没有过滤或转义掉非法字符
        jQuery.escapeHtml=function(s){
   	return (s)? jQuery("<p>").text(s).html(): "";}
	
   escapeHTML: function(a){  
       a = "" + a;  
       return a.replace(/&/g, "&").replace(/</g, "<").replace(/>/g, ">").replace(/"/g, """).replace(/'/g, "'");;  
   },
   ```

3. CSRF 跨站请求伪造

   ```js
   原因：服务器的所有参数都是预先构造的，根据拼接url发出请求
   手段：冒充用户 诱导用户向服务器发送请求
   预防：
       1.服务端的 CSRF 方式方法很多样,但总的思想都是一致的,就是在客
   户端页面增加伪随机数。
       2.使用验证码
   ```

4. XSS与CSRF有什么区别

   ```js
   XSS 是获取信息,不需要提前知道其他用户页面的代码和数据包。
   CSRF 是代替
   用户完成指定的动作,需要知道其他用户页面的代码和数据包。 
   要完成一次 CSRF 攻击,受害者必须依次完成两个步骤: 
   1.登录受信任网站 A,并在本地生成 Cookie。

   2.在不登出 A 的情况下,访问危险网站 B。
   ```

5. 自己在项目中有处理过哪些跨域问题？

   ```
   有，加分
   ```

6. https 对称加密和非对称加密 [https://zhuanlan.zhihu.com/p/27395037](https://zhuanlan.zhihu.com/p/27395037)



