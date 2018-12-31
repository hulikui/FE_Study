HTML渲染

1. HTML源码
2. 压缩解析
3. doctype html5 以及 编码显示utf-8
4. head标签中 link css
5. 继续加载body部分，载入HTML标签的同时，CSS已经具备，就开始渲染页面
6. img加载时，不阻塞，继续渲染
7. 如果改变了原有的位置，重新渲染
8. script 一直等待加载并且会阻塞其他渲染，加载执行完后继续
9. script 执行会引起 回流和重绘

这部分主要考察广度

```js
1，用过哪些HTML5的新特性，新标签
    canvas等等 
    input的新type

2，标签语义化的理解
    1. 便于人的理解，程序可阅读性强
    2. 利于SEO

3，HTML5 本地存储的新特性
    有：localStorage、localStorage(前两者大约最大 5 M 大小) 和 indexDB（后者一般上限是500 M）
    localStorage 和 localStorage的区别
        localStorage 永久存储
        sessionStorage 临时，浏览器该页面关闭后就立即失效
    localStorage的使用
        1：key-value 的形式存储 key 和 value 必须都为字符串
        2：localStorage[key] = 'value';

4，接着3问
    cookie 和 HTML5的 localStorage 有什么区别
    1. cookie 大小4 KB；localStorage 5 MB
    2. cookie 可以通过http协议自动传送至服务端与服务端进行交互
    3. 可以继续问cookie 包括哪些字段
    4. cookie的应用场景
        购物车
        用户登陆状态的维持等等

5, 接着4问 cookie 和 session 的区别
```



