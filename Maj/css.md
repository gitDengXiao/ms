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



##### link和import的区别？

1.浏览器执行到link会立即执行link的内容，而import引用的css会等到页面加载结束后加载

2link方式权重高于import的

3.link是html标签因此没有兼容性，而import只是ie5以上才能识别

##### rem

（font size of the root element）是指相对于根元素的字体大小的单位。简单的说它就是一个相对单位。看到rem大家一定会想起em单位，em（font size of the element）是指相对于父元素的字体大小的单位。它们之间其实很相似，只不过rem计算的规则是依赖根元素,em是依赖父元素计算

版权声明：本文为CSDN博主「MaJing_CUI」的原创文章，遵循CC 4.0 by-sa版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/MaJing_CUI/article/details/78855089

##### 水平垂直居中的方式有哪些？兼容IE6789

不定宽高div水平垂直居中

transfrom:translate(-50%,-50%);position:absolute;top:(50%);left:(50%)



##### 详细解释一下回流， 重绘

##### **transform、opacity、filters这些动画不会引起回流重绘** 

（回流必定将引起重绘，但是重绘不一定会引起回流）

##### 硬件加速（以及利弊）

css3d硬件加速 （通过GPU进行渲染，解放cpu。 ）

使用3D硬件加速提升动画性能时，最好给元素增加一个z-index属性，人为干扰复合层的排序，可以有效减少chrome创建不必要的复合层，提升渲染性能，移动端优化效果尤为明显。（页面建立了过多的复合图层，同样也会造成页面的卡顿 ）

大家可以现在就排查一下这类问题，尤其是用了轮播、动画loading的页面，出现这问题很常见。另外推荐在追查性能问题的时候打开『show composited layer borders』选项，如果页面有很多黄色的框肯定是不对的。

##### transition animation区别？ 

transition需要一个触发一个事件才能更改属性，而animation不需要触发，并且transition是from。。to为2帧，而animation可以一帧一帧的

- 开始事件: webkitAnimationStart
- 结束事件: webkitAnimationEnd
- 重复运动事件: webkitAnimationIteration
- transition 仅有这一个事件 webkitTransitionEnd

##### js动画和css3动画区别？

##### visibility=hidden, opacity=0，display:**none**

opacity=0，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的

visibility=hidden，该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件display=none，把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样 

##### px,em,rem

像素 px 是`相对于显示器屏幕分辨率`而言的 

em是相对长度单位 ,它会继承父级元素的字体大小，因此并不是一个固定的值 

rem相对html根元素

##### 换行字符串格式化

##### 屏幕占满和未占满的情况下，使footer固定在底部，尽量多种方法。

#####  两栏 三栏布局

##### 画一个0.5px的线条

##### 消除图片底部间隙

图片底线对齐 img{vertical-align:bottom;} 

图片块状化 - 无基线对齐 img{display:block;} 

行高足够小 - 基线位置上移 .box{line-height:0;} 