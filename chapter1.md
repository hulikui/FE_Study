# 1.CSS

1. 盒子模型 （content+padding+border+margin）
   1. W3C  content 不包括其他部分
   2. IE  content 包括 padding + border
       
      ```
         box-sizing
             content-box: width = content
             border-box: content+padding+border = width
         ```
   3. margin 塌陷
   
      ```
      <div class="parent">
          <div class="child"></div>
      </div>
      .parent {
          width: 200px;
          height: 200px;
          background: red;
      }
      .child {
          width: 100px;
          height: 100px;
          background: #000;
          margin-top: 10px;
      }
      child 块 main块并没有10px的距离
      ```
   4. 1. 为什么会发生？
         1. 两个或者多个边距没有被非空内容（paading, border, clear）分开
         2. 处于文档流中（float, obsoluate元素不会发生）, 本质上处于一个新的BFC就不会发生
      2. 解决办法
         1. 父级overflow: hidden
         2. 父级pading-top: xpx
         3. 父级position: absolute
         4. 父级display: inline-block
         5. 子元浮动与position: absolute
   5. marigin 上下合并
      1. 合并触发情形

          ```
            1. 水平margin不会合并。
            2. 两个上下渲染相邻（不一定是兄弟节点）的块状元素在正常页面流情况下会发生 margin 合并。
            3. 浮动元素不会和任何元素（包括子孙节点）发生 margin 合并。
            4. overflow！=visible的元素不和任何元素发生margin合并。
            5. 绝对定位的元素不和任何元素发生margin合并。
            6. inline-block 的元素不和任何元素发生margin合并。
            7. 设置 clear 属性的元素不和任何元素发生margin合并。
            8. 根元素不和任何元素发生margin合并。
            9. 父节点和第一个子节点发生margin-top合并。
            10. 如果最后一个子节点没有border以及padding，则和其父节点发生margin-bottom合并。

            ```

      2. 合并规则

         1. 都是正数或者0 取最大值

         2. 负数和正数 取相加

         3. 都是负数 取绝对值最大负数
   6. marigin 为负数时， 会向相反的方向移动，甚至覆盖在其他元素上
   7. BFC（块级格式上下文）
      1. 概念：一个接一个的垂直排列，水平方向撑满整个宽度的一种布局
      2. 如何创建
          ```
            float不为none
            overflow不为visible
            position为absolute或者fixed
            display:inline-block table-cell table-caption
            ```
      3. 作用
         1. 清楚内部浮动（子元素设置浮动，父级元素高度塌陷height:0 overflow: hidden）

         2. 垂直margin合并

         3. 容器独立

         4. 创建自适应两栏布局

            1. ```
               <style>
                   body {
                       width: 300px;
                       position: relative;
                   }
 
                   .aside {
                       width: 100px;
                       height: 150px;
                       float: left;
                       background: #f66;
                   }
 
                   .main {
                       height: 200px;
                       background: #fcc;
                       overflow: hidden;
                   }
               </style>
               <body>
                   <div class="aside"></div>
                   <div class="main"></div>
               </body>
               ```
2. CSS经典布局

   1. 圣杯布局

       ```
         <style>
             .left,
             .middle,
             .right {
                 position: relative;
                 float: left;
                 min-height: 200px;
             }
             .container {
                 padding: 0 220px 0 200px;
                 overflow: hidden;
             }
             .left {
                 margin-left: -100%;// 向左移动 父元素的宽度 到达最左边
                 width: 200px;
                 left: -200px
             }
             .right {
                 margin-right: -100%;
                 width: 220px；
             }
             //
             .right {
                 margin-left: -220px
                 width: 220px;
                 right: -220px
             }
         </style>

         <div class="container">
             <div class="middle">// 优先加载渲染最重要的部分
                 <h4>middle</h4>
             </div>
             <div class="left">
                 <h4>left</h4>

             </div>
             <div class="right">
                 <h4>right</h4>
             </div>
         </div>
         ```

  2. 双飞翼布局

          ```
            <style>
                .main,
                .sub,
                .extra {
                    float: left;
                    min-height: 200px;
                }
                .main {
                    width: 100%;
                }
                .main-inner {
                    margin: 0 220px 0 200px;
                }
                .sub {
                    margin-left: -100%;
                    width: 200px;
                }
                .extra {
                    margin-left: -220px;
                    width: 220px;
                }
            </style>
            <div class="main">
                <div class="main-inner">
                    <h4>main</h4>
                </div>
            </div>
            <div class="sub">
                <h4>left</h4>
            </div>
            <div class="extra">
                <h4>right</h4>
            </div>
            ```

 2. 由BFC启发的布局 侧面布局优先加载

            1. 参考BFC讲解-两栏布局

            2. 三栏布局中间自适应

                ```
                  <style>
                      .left,
                      .main,
                      .right {
                          height: 200px;
                      }
                      .left {
                          float: left;
                          width: 200px;
                      }
                      .right {
                          float: right;
                          width: 200px;
                      }
                      .main {
                          padding: 0 200px;
                          width: 100%;
                      }
                  </style>
                  <div class="left">
                      <h4>left</h4>
                  </div>
                  <div class="right">
                      <h4>right</h4>
                  </div>
                  <div class="main">
                      <h4>main</h4>
                  </div>
                  ```
3.    绝对居中的几种方法
4.    CSS属性重要区别
    1.    position
        1.    relative 相对于自身的原来的正常位置
        2.    absolute 相对于第一个非static的父级元素
            ```
                1.使得inline元素被块状化
                2.层级元素后来者居上
                3.会使float失效
            ```
    2.    rem、em、px
        1.    rem 相对于html根元素的font-size
        2.    em  相对于父级元素的font-sze
        3.    px 绝对大小 16px rem em相对大小
                  
                  
                  




