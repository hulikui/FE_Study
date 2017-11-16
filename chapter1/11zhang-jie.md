# 1.CSS

1. 盒子模型 （content+padding+border+margin）  
   1. W3C  content 不包括其他部分  
   2. IE  content 包括 padding + border

   ```css
     box-sizing
       content-box: width = content
       border-box: content+padding+border = width
   ```

   1. margin 塌陷

      ```css
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

   2. 1. 为什么会发生？
         1. 两个或者多个边距没有被非空内容（paading, border, clear）分开
         2. 处于文档流中（float, obsoluate元素不会发生）, 本质上处于一个新的BFC就不会发生
      2. 解决办法
         1. 父级overflow: hidden
         2. 父级pading-top: xpx
         3. 父级position: absolute
         4. 父级display: inline-block
         5. 子元浮动与position: absolute
   3. marigin 上下合并  
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

      1. 合并规则

         1. 都是正数或者0 取最大值

         2. 负数和正数 取相加

         3. 都是负数 取绝对值最大负数

   4. marigin 为负数时， 会向相反的方向移动，甚至覆盖在其他元素上

   5. BFC（块级格式上下文）  
      1. 概念：一个接一个的垂直排列，水平方向撑满整个宽度的一种布局  
      2. 如何创建

      ```
            float不为none
            overflow不为visible
            position为absolute或者fixed
            display:inline-block table-cell table-caption
      ```

      1. 作用  
         1. 清楚内部浮动（子元素设置浮动，父级元素高度塌陷height:0 overflow: hidden）

         1. 垂直margin合并

         2. 容器独立

         3. 创建自适应两栏布局

            1. ```css
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

      ```css
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
             .middle {
                 width: 100%;
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

      ```css
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

   3. 由BFC启发的布局 侧面布局优先加载

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

   4. 左右两侧自适应，中间固定

      1. flex

   5. 1. ```
         <style>
             .parent {
                 display: flex;
             }
             .left,
             .right {
                 flex: 1;
             }
             .mid {
                 width: 200px;
             }
         </style>
         <div class="parent">
             <div id="left">
                 <div class="container">
                     left 宽度自适应
                 </div>
             </div>
             <div id="mid">
                 mid 宽度固定 : 200px
             </div>
             <div id="right">
                 <div class="container">
                     right 宽度自适应
                 </div>
             </div>
         </div>
         ```
      2. css2解决办法

         1. ```
            <style>
                .mid,
                .left,
                .right {
                    position: absulte;
                    top: 0;
                }
                .left,
                .right {
                    width: 50%;
                }
                .left .container {
                     margin-right: 300px;
                }
                .right .container{
                     margin-left: 300px;   
                }
                .left {
                    left: 0;
                }
                .right {
                    right: 0;
                }
                .mid {
                    width: 600px;
                    left: 50%;
                    top: 0;
                    margin-left: -300px;
                }
            </style>
            <body>
                <div class="mid">
                    mid
                </div>
                <div class="left">
                    <div class="container">
                        left
                    </div>
                </div>
                <div class="right">
                    <div class="container">
                        right
                    </div>
                </div>
            </body>
            ```

3. 绝对居中的几种方法

4. CSS属性重要区别  
   1. position  
      1. relative 相对于自身的原来的正常位置  
      2. absolute 相对于第一个非static的父级元素

   ```
         1.使得inline元素被块状化
         2.层级元素后来者居上
         3.会使float失效
   ```

   1. rem、em、px
      1. rem 相对于html根元素的font-size
      2. em  相对于父级元素的font-sze
      3. px 绝对大小 16px rem em相对大小
   2. display
      1. inline-block 可以设置宽高
      2. table 带有前后换行
   3. line-height
      1. 父级元素有单位 父级元素的font-size \* xem 或者 直接应用px
      2. 父级元素没有单位 子元素的font-size \* line-height 倍数 = 子元素的行高
   4. css选择器权值计算公式  
      1. style内联   1000  
      2.  \# ID   100  
      3. .类和伪类和属性选择器    10  
      4. 标签和伪元素    1  
      5. \*通用 和 相邻 +  无视  0

      ```
      /* 这个相邻选择器由标签选择器与属性选择器组成，属性选择器为10 */
      ul ol li.red {} /* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 */
      ```

   5. display: none 、visibility: hidden、 opacity:0

      1. 前者不渲染 后两者浏览器渲染



