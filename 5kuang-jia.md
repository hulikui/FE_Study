1. 框架MVC 和 MVVM的区别
2. angular框架  
   1. 脏检查机制  
      1. 将原对象赋值一份快照。在某个时间事件触发遍历比较当前对象和快照，如果不一样就执行某些操作  
      2. 流程  
         1. \`\`\`  
            1，绑定ng事件的DOM 创建一个watcher对象  
            2，每创建一个watcher对象就会被push到$scope.$$watchers队列，脏检查就是遍历这个数组  
            触发的函数  
            $digest 遍历当前域以及子域的watchers  
            $apply 从$rootScope开始  
            一次脏检查中 digest 至少会执行两次 超过10次会报错

   ```
      3. 触发条件

         1.
   ```

            controller 初始化
            几乎所有ng-开头的事件(ng-click,ng-change...)
            http请求
            $timeout,$interval
            手动调用$apply(), $digest()
            ```

3. [react框架](https://github.com/bailicangdu/react-pxq)
   1. diff算法
      ![](https://segmentfault.com/img/bVuH57)
   2. redux
      1. ![](https://github.com/bailicangdu/pxq/raw/master/src/images/all_redux.png)
      2. 



