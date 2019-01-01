# 前端基本知识

1. [CSS](/chapter1.md)
   ```css
   1. 盒模型 box-sizing: content-box; border-box;
   2. display: block; inline-block; none;
   3. position: relative; absolute; fixed; 
   4. margin塌陷 （父子） marigin合并（兄弟） top bottom
   5. 优先级 !important > 内联 > id > class > span | 选择器 > 通配
   6. 动画1s 60帧 transition 性能 transform 
   7. visibility: hidden; 和 display: none 的区别
   8. 经典布局 记不住但要说目的 渲染至上而下
   9. less 块级作用域，变量等
   ```
2. [HTML](/html.md)
   ```css
   1. doctype html 代表 html5
   2. 新标签语义化 SEO
   3. 加载和渲染顺序 head内 script会阻塞html标签的渲染 html标签 DOMTree -> CSS CSSOM -> renderTree -> 几何布局 -> 绘制
   4. script 的 async 异步执行 DOMContentLoaded 后 defer 延迟执行，但是所有资源都加载完
   5. 表单序列化
   ```
3. [JavaScript](/javascript.md)
   ```js
   1. 闭包
   2. this 调用
   3. apply call bind 
   4. 原型链的定义 实例对象的__proto__ 指向构造函数的原型对象prototype，接着其狗仔函数的原型对象的__proto__ 也指向其构造函数
   的原型，直到为null为止
   5. 简单的继承类 原型链继承：需要拷贝的定义在函数内，需要共享的方法，放在原型对象里
   6. Promise 即“承诺一定会执行”，回调方法的一种链式调用，其原理就是在then时把成功回调函数赋值，resolve调用这个回调，实现一个
   最容易的
   7. setTimeout 和 setInterval
       setTimeout 当前同步任务和事件队列所有事物处理完才会运行，会在下一次的event-loop运行
       setInterval每段时间内执行，如果其中执行时间超过了定义的时间，就会忽略这次执行，进入下一个循环
   8. 注意些变量提升，函数提升
   9. 简单数据类型以及复杂引用数据类型
   10. 怎么复制对象，浅拷贝 以及 深拷贝的实现
   11. ES6 新知识
       解构赋值（只识别undifined）、块级作用域、箭头函数、class类、Set 和 Map以及其他扩展的方法等等
   12. 值传递
   13. 路由实现原理：history.pushState(null, null, url) 和 onhashchange监听hash #
   14. JSONP 实现原理
   15. AJAX 实现
   16. 同源策略 以及 跨域解决方法 window.domain、postMessage、CORS跨域资源共享 access-control-allow-method
   17. 如何链式调用 return this;
   18. 模块 单例即执行函数 -> node commonjs(同步) -> web的 AMD 异步模块定义 依赖前置 -> CMD 按需加载 -> ES6 modules 
       -> webpack 自定义的兼容打包模块
   19. require 和 ES6 moudles的区别
       require 值的拷贝，有缓存只加载一次，动态加载，输出的是个对象 或者 常量等
       es6 modules 是引用，编译时加载，默认严格模式，输出的是解构等，值的引用
   20. 垃圾回收机制 标记清除 和 引用计数
   ```
4. [安全](/4an-quan.md)
   ```
   1. xss cross-site script 跨站脚本攻击
       base64 onerror
       escapeHtml
   2. csrf cross-site request forgery 跨站请求伪造
       cookie 诱导 请求参数可以预先构造
       随机数验证码 origin
   3. sql注入
   ```
5. [HTTP协议](/http.md)
   ```js
   1. 三次握手 和 四次握手
   2. 1.1 connect: keep-alive 状态保持 以及 双工 2.0 服务端推送
   3. https 加密 对称加密 和 非对称加密
       三次握手后获取服务器证书以及公钥-> 产生随机数以及约定对称加密算法，并提取hash防止篡改->服务端私钥解密，并用对称加密
   4. 缓存 强缓存 和 协商缓存
       强缓存：expires GMT 时间戳、cache-control: public,private 范围；max-age: 200s; no-cache 放弃强缓存；200from cache
       协商缓存：last-modified 和 if-since-modified 秒级更新，时间有误差, 时间更新但实际无更新；304命中
           Etag 和 if-none-match md5 提取
   5. host 目标服务器 中间可能经过代理服务器；origin 跨域验证；referer 防盗链，上次location.href
   ```
6. [框架](/5kuang-jia.md)
   ```js
   1. React特性 jsx语法，组件，虚拟DOM
   2. React组件通信 父子通信通过回调函数，或者 系统监听函数；兄弟组件无法直接通信；所以Redux解决组件通信问题
   3. React diff 算法 O(n) 
       tree diff 同一层级比较；component diff 类型不同直接替换；element diff 直接对比key 无key 直接对比
   4. 如何更新React组件 this.setState 调用 render方法；PureComponent shouldComponentUpdate 浅比较 true 就调用render
    redux 通过connect封装一层组件，在componentDidMount 监听store 数据是否变化，无变化再浅比较 mapstateprops ，有变化直接
    this.setState 调用render 进行更新子组件
   5. React 生命周期
    初始化5个 、 更新阶段5个、销毁1个
   6. 性能问题，纯渲染组件用function component 或者 pureComponent、state树层级不能太深、组件层级不能太深，全部打平
   、少用生命周期
   7. setIn 利用内存；Object.assign; 防止pureComponent无更新
   ```
7. [算法](/suan-fa.md)
8. [缓存](/huan-cun.md)
9. 性能优化
   ```js
   技术上的性能优化
   1. css 避免重绘和重排；@import影响并行下载；性能优化动画 打包 雪碧图
   2. script link 适当多用cdn 浏览器多线程加载 webpack externals 全部变量 + CDN
   3. 图片压缩、js/css 压缩以及 html文本压缩
   4. css dom 以及 脚本放置位置 和 模块按需加载
   5. 使用 缓存技术
   6. 代码本身时间复杂度的优化、内存及时释放、闭包什么的 很难衡量
   7. 打包本身的取舍，css浏览器的兼容程度对体积影响较大
   体验上的
   1. 首屏渲染慢 适当使用SSR
   2. 适当使用 loading 动画 以及占位符 以及 使用布局把重要的内容放在前面，优先加载
   ```

```js
前端主要考察知识点的广度和JavaScrpt语言的深度
1. JavaScript
2. 常用 HTTP 知识点以及调试工具的掌握
3. 对浏览器安全策略的理解 
4. 前端工程化 工具的使用
5. （最重要）为什么要学前端，前端什么吸引你？做过哪些值得自己骄傲的项目？怎么学习的前端？
```



