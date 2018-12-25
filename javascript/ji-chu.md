1. JavaScript 是 单线程还是多线程？

   ```js
   JS 是单线程的（这个搞不清楚就可以fail掉了）
   延伸下：为什么浏览器JS要设置为单线程 而不是其他 多线程 的
       无非是初期浏览器性能问题，单线程尽可能的快而不过多占用系统资源

   JS 是 异步非阻塞的，解释下这个概念
       1，JS代码是顺序执行，但是遇到一些异步事件（比如网络请求，I/O，setTimeout函数、Node.js的数据库操作等等）会把这些事件放入一个事件队列，然后尽快执行其后面的代码；
       2，直到JS代码执行完毕后，开始处理事件队里里的异步事件，每个异步事件执行成功后再去执行回调（通知CPU或者主函数执行完毕继续执行下一步代码）
       3，这样直到所有代码执行完毕的过程（尽可能的让CPU和硬件利用起来）
       console.log(1);
       setTimeout(function(){
           console.log(2);
       }, 0);
       for (var i = 0; i < 100; i++);
       console.log(3);
       //正确输出结果是： 1 3 2 
   JS的优缺点：
       擅长异步I/O，但是不擅长大量计算
   ```

2. JavaScript 基本数据和引用类型
   ```js
   1. js基本数据类型:
   Number、String 、Boolean、Null和 undefined
   2. 基本引用类型: Object 、Array 、Function 、Date和（ES6的RegExp(正则)）
   ```
3. null  和 undifined 的区别

   ```js
   null是一个表示"无"的[对象],转为数值时为0 即(Number(null) == 0);
   undefined是一个表示"无"的原始值,转为数值时为NaN 即(Number(undifined) == NaN)。
   当声明的变量还未被初始化时, 变量的默认值为undefined。
   null 用来表示尚未存在的对象,常用来表示函数企图返回一个不存在的对象。
   ```

4. == \(双等于\) 和 === \(全等于\) 的区别

   ```js
   双等于比较的时候会进行类型转换，比如
     "1" == 1 // true
     全等于严格比较两者的值，即
     "1" === 1 // false
     但是JS 有个特殊的现象即：NaN == NaN // false
     NaN === NaN // false NaN 和自己不相等 这是规定
   引用类型的值 因为引用类型的值指向 内存地址的值 所以这一点值得注意
     var a = []; var b = a;
     a.push(1);
     a === b;// true    a 和 b 都指向同一个地址
   ```

5. 同上引申的一个问题，怎么比较两个数字数组A和B是否相同

   ```js
   1，首先判断两者是否是数组 利用 Array.isArray(A) && Array.isArray(B)判断;
   2，再次检查 A.toString() === B.toString() 是否相等即可
   ```

6. javascript 的 this 关键字

   ```js
   1. 定义：this 是 Javascript语言的一个关键字。 它代表函数运行时,自动生成的一个内部对象,只能在函数内部使用. 
      随着函数使用场合的不同,this的值会发生变化。但是有一个总的原则, 那就是this指的是, 调用函数的那个对象。
   2. js中的this有四种调用模式(程序输出题): 
         1.方法调用模式:当一个函数被保存为一个对象的属性,这个方法被调用时,this指向该对象。 
            var obj = { 
               name: 'Likui', 
               sayName: function() { 
                  console.log(this.name) 
               } 
            } 
            obj.sayName(); // 输出 'Likui' 
         2.函数调用模式: 当一个函数直接被调用 window
            var name = "window"; 
            var obj = {
               name: 'Likui',
               sayName: function() {
                  console.log(this.name) 
                  } 
               } 
            var say = obj.sayName; // 赋给变量 
            say(); // 实际是 window.say(); 调用者是 window, obj.sayName 函数的 this指向window全局, 输出name: window
   3.构造器调用模式:在构造函数内部,this指向新创建的对象。 
   4.apply 和 call 调用模式:函数内部this会被设置为传入的第一个参数
   ```

7. 闭包

   ```js
   JS闭包的特征:
   1. 可以访问外部函数作用域中的变量
   2. 被内部函数访问的外部函数的变量可以保存在外部函数作用域内而不被回收---这是核心,

   总结闭包的优缺点：
   优点： 
   1.可以让一个变量常驻内存 (如果用的多了就成了缺点)
   2.避免全局变量的污染
   3.私有化变量

   缺点：
   1.因为闭包会携带包含它的函数的作用域,因此会比其他函数占用更多的内存
   2.引起内存泄露
   ```

8. apply 和 call 的区别

   ```js
   所有函数都有两个方法：
   Function.prototype.apply 和 Function.prototype.call
   1，两者都返回的是一个新的函数（提前可以给这个新的函数绑定参数，如下）
   2，两者获取参数的形式不同
       Function.prototype.apply(context, [参数1，参数2，...]) 第二个参数是数组
       Function.prototype.call(context, 参数1，参数2，...) 参数不固定
   ```

9. ajax请求（get请求 和 post请求的区别）

   ```js
   1, get 参数 携带在url上，http 请求体body 数据为空，post 数据携带在http请求体body上
   2，post 参数携带大小无限制，但是get请求的url长度有限制
   3，post 比 get 更安全一点，但是也只是看上去安全，因为Http是明文传输
   ```

10. 前端跨域问题

    ```js
    ￼1. jsonp 
        原理：(jsonp的原理是动态插入script标签, 利用script的src 加载 绕过浏览器检查) 
        缺点是：只能是get请求 
    2. 服务器跨域资源共享（CORS）设置Http请求头，允许跨域
    3. document.domain+iframe、window.name、window.postMessage等等
    ```

11. （备选加分）有没有用过ES6（JavaScript 的语言标准 改善了ES5的许多诟病）

    ```
    假如用过继续问：有没有用过比如 gulp、Webpack等前端构建工具
    因为主流浏览器主要兼容ES5，很多浏览器不支持ES6，需要利用打包工具把ES6转化为ES5语言
    ```

12. \(备选加分\) 有没有用过 Node.js

    ```
    Node.js 相当于Java语言的JVM，跨平台、即在服务器上运行JavaScript代码
    基于Node.js一般的项目：后端框架是 Express 或者 Koa
    数据库：非关系型数据库Mongodb 和 关系型数据库 Mysql
    这些后端共同的知识点可以在这里延伸下。
    ```



