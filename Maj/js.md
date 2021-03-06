 clearTimeout(timer)  和 timer = null

```js
var x = setInterval(function(){
    alert()
    x = null;
},1000);
```

主机名.次级域名.顶级域名.根域名
www.example.com.root

立即执行函数作用
1，隔离作用域
2，

```js
        typeof NaN // "number"

        0.5 + 0.1 == 0.6 //true
        0.1 + 0.2 == 0.3 //false  

        Math.max() //-Infinity
        Math.min() //Infinity

        [] + [] // ""
        [] + {} //"[object Object]"
        {} + [] //0

        true + true + true === 3 // true
        true - true // 0
        true == 1 // true
        true === 1 // false

        9 + "1" // "91"
        9 - '1' // 8
        [] == 0 // true

//js里的隐式的rule
//js在进行加法运算的时候， 会先推测两个操作数是不是number。 
//如果是，则直接相加得出结果。 
//如果其中有一个操作数为string，则将另一个操作数隐式的转换为string，然后进行字符串拼接得出结果。 
//如果操作数为对象或者是数组这种复杂的数据类型，那么就将两个操作数都转换为字符串，进行拼接 
//如果操作数是像boolean这种的简单数据类型，那么就将操作数转换为number相加得出结果

//parseInt函数 (如果参数不是一个字符串，则将其转换为字符串。字符串开头的空白符将会被忽略)
```

##### js异步方法

1.回调

2.事件监听

3.发布、订阅

4.promise

5.await

```js
//因为 setTimeout() 不是异步函数， await 对它没作用的
async function Func(){
        let b = 0
        b = await setTimeout(function(){return 20},3000)
        return b // 这一行并不会 3 秒后才执行，而是立即执行
      }
      
  setInterval(()=>{Func().then(res=>console.log(res))},1000)//依次为12,13,14,15...
```

**sleep函数**

<https://muyiy.cn/question/program/42.html> 

##### js sort() 方法原理以及使用

<https://www.jianshu.com/p/214627f54367> 

##### 堆栈溢出、尾调用、尾递归、setTimeout不会堆栈溢出？

##### **Object.create(),{},new object()**

```js
var obj ={a: 1}
var b = Object.create(obj)
console.log(obj.a) // 1
console.log(b)  // {}
console.log(b.a) // 1
b.a = 2
console.log(obj.a)
//Object.create()返回了一个新的空对象，并且这个空对象的构造函数的原型（prototype）是指向obj的。所以当我们访问新对象b.a的时候实际上是通过原型链访问的obj中的a

//Object.create(null) 会创建一个真正的空对象，并没有继承Object原型链上的方法
//var a = {} 这并不是一个纯粹的空对象，它会继承原型链上的很多方法
```



##### ajax面试

```js
1.创建XMLHttpRequest对象
	var xhr = new XMLHttpRequest()
2.设置请求参数
	xhr.open(请求方式，请求地址，异步或同步)
3.设置回调
    xhr.onreadystatechange = function(){
        if(xhr.reasyState===4){
                if(xhr.status === 200) {
                    //5、接受响应
                    console.log(xhr.responseText);
                }
            }
    }
4、发送请求
    xhr.send()
```

**字符串加减**



**valueof** **tostring**（类型转换）

+号作为一元运算符----在这个情况下，对象基本数据类型的装换规则是：调用对象的toString或者valueOf函数，将对象转化为基本数据类型的值 ，那么到底是调用toString()还是 valueOf()？

```js
// https://www.jianshu.com/p/c1872ec363cb
//关于(a ==1 && a== 2 && a==3) 值为true
var b = 0
var a = {
    valueOf(){
        return b+=1
    }
}
if(a == 1 && a==2 && a== 3){
    console.log('true')
}
//https://juejin.im/post/5a63f9a451882573473ddba4
```



##### indexOf 和  lastIndexOf 是什么？

indexOf 和 lastIndexOf 都是索引文件

indexOf 是查某个指定的字符串在字符串首次出现的位置（索引值） （也就是从前往后查）

lastIndexOf 是从右向左查某个指定的字符串在字符串中最后一次出现的位置（也就是从后往前查）

##### IIFE是什么？优缺点

立即执行函数表达式 

创建块级（私有）作用域，避免了向全局作用域中添加变量和函数 

IIFE中定义的任何变量和函数，都会在执行结束时被销毁 

##### 如何理解前端模块化

##### 详细解释事件循环，事件委托，冒泡，捕获等



##### Event核心类，on,off,once,trigger实现

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

##### **数组的方法**

**不改变原数组：**
1、concat()   连接两个或多个数组，并将新的数组返回，不改变原数组，返回新的数组

2、join()   把数组中所有元素放入一个字符串，将数组转换为字符串，不改变原数组，返回字符串

3、slice()  从已有的数组中返回选定的元素，提取部分元素，放到新数组中，参数解释：1：截取开始的位置的索引，包含开始索引；2：截取结束的位置的索引，**不包含结束索引。不改变原数组**，返回一个新数组

4、toString()   把数组转为字符串，不改变原数组，返回数组的字符串形式

**改变原数组：**
5、pop()  删除数组最后一个元素，如果数组为空，则不改变数组，返回undefined，改变原数组，返回被删除的元素

6、push()   向数组末尾添加一个或多个元素，改变原数组，返回新数组的长度

7、reverse()   颠倒数组中元素的顺序，改变原数组，返回该数组

```js
string.split('').reverse().join('') 
//字符串反转
//https://muyiy.cn/question/program/81.html
```

8、shift()   把数组的第一个元素删除，若空数组，不进行任何操作，返回undefined,改变原数组，返回第一个元素的值

9、sort()   对数组元素进行排序，改变原数组，返回该数组

10、splice()   从数组中添加/删除项目，改变原数组，返回被删除的元素(**数组**)

11、unshift()   向数组的开头添加一个或多个元素，改变原数组，返回新数组的长度 



##### 如何对一个url查询参数转换成数据字典

##### 数组去重（求数组交集，并集，差集）

<https://blog.csdn.net/u010003835/article/details/79042135> 

```js
        // let a = [1, 2, 3],
        //     b = [2, 3, 4, 5]
Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。
Set类似于数组，区别在于它所有的成员都是唯一的，不能有重复的值
        // console.log(Array.from(new Set(a.concat(b)))) 并集(es6)
        // let newArray = a.filter(item => {
        //    return b.includes(item)
        // })
        // console.log(newArray)  交集(es7)

        // let aSet = new Set(a)
        // let bSet = new Set(b)
 
        // let newArray = Array.from(new Set(a.filter(item=>{
        //     return bSet.has(item)
        // })))

        // console.log(newArray)  交集（es6）
```

为啥 await 不能用在 forEach 中

**reduce** （<https://www.jianshu.com/p/e375ba1cfc47> ）

**reduce去重，降维，求和**

##### 手写 排序（冒泡，快排）

##### 手写 防抖节流

##### 手写 深拷贝














