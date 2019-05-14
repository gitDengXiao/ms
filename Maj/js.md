##### indexOf 和  lastIndexOf 是什么？

indexOf 和 lastIndexOf 都是索引文件

indexOf 是查某个指定的字符串在字符串首次出现的位置（索引值） （也就是从前往后查）

lastIndexOf 是从右向左查某个指定的字符串在字符串中最后一次出现的位置（也就是从后往前查）

##### IIFE是什么？

立即执行函数表达式 

创建块级（私有）作用域，避免了向全局作用域中添加变量和函数 

IIFE中定义的任何变量和函数，都会在执行结束时被销毁 

##### 如何理解前端模块化

##### 详细解释事件循环，事件委托，冒泡，捕获等



##### Event核心类，on,off,once,trigger实现

##### a = 3, b = a , b = 5 console.log(a) // 3 为什么？

精度丢失

计算机中的数字都是以二进制存储的，如果要计算 0.1 + 0.2 的结果，计算机会先把 0.1 和 0.2 分别转化成二进制，然后相加，最后再把相加得到的结果转为十进制。

但有一些浮点数在转化为二进制时，会出现无限循环。比如，十进制的 0.1 转化为二进制，会得到如下结果：

``` 
0.0001 1001 1001 1001 1001 1001 1001 1001 …（1001无限循环）
```

解决思路，把浮点数转为字符串

##### 如何让子类继承父类的所有方法和属性？

**八大数据解构**：

数组

链表

栈：栈是一种特殊的线性表，仅能在线性表的一端操作，栈顶允许操作，栈底不允许操作。 栈的特点是：先进后出，或者说是后进先出，从栈顶放入元素的操作叫入栈，取出元素叫出栈

队列：队列可以在一端添加元素，在另一端取出元素，也就是：先进先出。从一端放入元素的操作称为入队，取出元素为出队

堆：

树：**树**是一种数据结构，它是由n（n>=1）个有限节点组成一个具有层次关系的集合。 

散列表（哈希表 ）：

图

##### 如何对一个url查询参数转换成数据字典

##### 数组去重

##### 日期转化为2小时前，1分钟前等
