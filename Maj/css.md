##### BFC是什么？

块格式化上下文 (CSS2.1规范 ),是页面css视觉渲染的一部分，用于决定块盒子的布局及浮动相互影响范围的一个区域（BFC就是页面上的一个隔离的独立容器 ）

BFC创建：

**根元素**或其它包含它的元素；

**浮动** (元素的float不为none)；

**绝对定位元素** (元素的position为absolute或fixed)；

**行内块**

**表格单元格**

overflow的值不为visible的元素；

**弹性盒 flex boxes** (元素的display: flex或inline-flex`)；



##### 水平垂直居中的方式有哪些？兼容IE6789

##### 详细解释一下回流， 重绘

（回流必定将引起重绘，但是重绘不一定会引起回流）

##### 硬件加速（以及利弊）

css3d硬件加速 （通过GPU进行渲染，解放cpu。 ）

使用3D硬件加速提升动画性能时，最好给元素增加一个z-index属性，人为干扰复合层的排序，可以有效减少chrome创建不必要的复合层，提升渲染性能，移动端优化效果尤为明显。（页面建立了过多的复合图层，同样也会造成页面的卡顿 ）

大家可以现在就排查一下这类问题，尤其是用了轮播、动画loading的页面，出现这问题很常见。另外推荐在追查性能问题的时候打开『show composited layer borders』选项，如果页面有很多黄色的框肯定是不对的。

##### 监听transition animation 

- 开始事件: webkitAnimationStart
- 结束事件: webkitAnimationEnd
- 重复运动事件: webkitAnimationIteration
- ransition 仅有这一个事件 webkitTransitionEnd



##### 换行字符串格式化

##### 屏幕占满和未占满的情况下，使footer固定在底部，尽量多种方法。

##### 左中右 上中下 两栏 三栏布局