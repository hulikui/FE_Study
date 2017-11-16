1. 盒子模型的含义

   ```css
   1. 盒子模型又称框模型(BoxModel) ,包含了元素内容(content)、内边距(padding)、边框(border)、外边距(margin)几个要素;
   2. box-sizing 属性有:
          content-box: (默认值):
              即总宽度 = margin + border + padding + content的width;
          ￼border-box: 
              总宽度 = border + padding + 内容的总宽度。

      inherit: 规定应从父元素继承 box-sizing 属性的值
   ```

   ![](http://www.runoob.com/images/box-model.gif)

2. float浮动的知识点

   ```css
   概念:浮动元素脱离文档流,不占据空间。浮动元素碰到包含它的边框或者浮动元素的边框停留
   1.使用空标签清除浮动。这种方法是在所有浮动标签后面添加一个空标签定义css: clear:both. 弊端就是增加了无意义标签。
   2.使用overflow。给包含浮动元素的父标签添加css属性: overflow:auto; zoom:1; (zoom:1用于兼容IE6)。
   3.使用:before和:after伪对象 清除浮动。
   ```

3. display: none 和 visibility: hidden 的区别

   ```css
   display:none 隐藏对应的元素,在文档布局中不再给它分配空间,浏览器不会渲染。
   visibility:hidden 隐藏对应的元素,但是在文档布局中仍保留原来的空间, 实际存在。
   ```

4. CSS优先级（根据优先级解决样式冲突）

   ```css
   !important > 内联样式 > ID > (类 | 伪类 | 属性选择) >(标签 | 伪元素) > 继承 > 通配
   ```

5. position定位属性有哪些？

   | 值 | 描述 |
   | :--- | :--- |
   | absolute | **生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。**元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
   | fixed | 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
   | relative | 生成相对定位的元素，相对于其正常位置进行定位。因此，"left:20" 会向元素的 LEFT 位置添加 20 像素。 |
   | static | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 |
   | inherit | 规定应该从父元素继承 position 属性的值。 |

6. （备选 加分）有没有用过 less 和 sass 这些CSS预处理

   ```
   与CSS的区别
   ```





