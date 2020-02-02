面向过程

概念：（百度百科）就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候，一个一个一次调用就可以了。

面向过程其实是最为实际的一种思考方式，就算是[面向对象](https://baike.baidu.com/item/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)的方法也是含有面向过程的思想。可以说面向过程是一种基础的方法。它考虑的是实际地实现。一般的面向过程是从上往下步步求精，所以面向过程最重要的是模块化的思想方法。对比面向过程，面向对象的方法主要是把事物给对象化，对象包括属性与行为。当程序规模不是很大时，面向过程的方法还会体现出一种优势。

面向对象（OOP）

概念：是把构成问题事物分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描述某个事物在整个解决问题的步骤中的行为。

三大特征：

1，封装

​	把客观事物封装为抽象的类，隐藏属性和方法，仅对外公开访问方式，提高复用性及安全性

​	

```js
function Person(){
            this.name = 'lisi'
        }
        // __proto__,constructor 属性是对象所独有的
        // prototype 属性是函数所独有的
        // https://blog.csdn.net/cc18868876837/article/details/81211729
        Person.prototype.age = 1 //通过原型prototype定义的属性或者方法，所有实例均指向同一个内存地址
        let p1 = new Person()
        let p2 = new Person()
        p1.name = 'zs' //（构造函数）证明通过this定义的属性和方法，我们实例化的时候都会重新复制一份，可能造成内存浪费
        p1.__proto__.age = 2
        console.log(p1)
        console.log(p2)

//虽然很多人都已经了解了new的实质，那么我还是要再说一下new 的实质 var o = new Object()

//1新建一个对象o
//2o. __proto__ = Object.prototype 将新创建的对象的__proto__属性指向构造函数的prototype
//3将this指向新创建的对象
//4返回新对象，但是这里需要看构造函数有没有返回值，如果构造函数的返回值为基本数据类型string,boolean,number,null,undefined,那么就返回新对象，如果构造函数的返回值为对象类型，那么就返回这个对象类型
function F1() {
    this.name = 'f1';
}

console.log(new F1()); // {name: "f1"} 返回实例, 委托原型
console.log(new F1().name); // f1

console.log(F1().name); // Uncaught TypeError: Cannot read property 'name' of undefined
console.log(F1()); // undefined
//例子二 函数返回引用类型值
function F2() {
    this.name = 'f2';
    return {};
}

console.log(new F2()); // 引用类型值, 返回该值{} 
console.log(new F2().name); // undefined

// 这种情况，使用new调用就与调用正常函数一致
console.log(F2()); // {} 常规函数调用
console.log(F2().name); // undefined
//例子三 函数返回基本类型值
function F3() {
    this.name = 'f3';
    return 5;
}

// 这种情况, 使用new调用函数就与调用标准构造函数一致
console.log(new F3()); // 基本类型值, 仍旧返回构造函数的实例 {name: f3}
console.log(new F3().name); // f3

console.log(F3()); // 5 常规函数调用
console.log(F3().name); // undefined
```

2，继承

子类可以使用父类的所有功能，并且对这些功能进行扩展。提高代码复用，继承是多态的前提。

<https://juejin.im/post/5b8a8724f265da435450c591#heading-11> 

```js
      //  原型链继承 
      //  构造函数继承 
        function Person() {
            this.name = '邵威儒'
            this.pets = ['旺财', '小黄']
        }

        Person.prototype.eat = function () {
            console.log('吃饭')
        }

        let p = new Person()


        function Student() {
            // Person.call(this) //利用call调用Person上的属性方法拷贝一份到Student ，即可解决下面的注释
            this.num = "030578000"
        }

        Student.prototype = p

        let stu = new Student()
        let stu2 = new Student()

        console.log(stu2.pets)

        stu.pets.push('小红') // 所有实例共享原型对象同一个属性方法，如果原型对象上有引用类型，那么会被所有实例共享，也就是某个实例更改了，则会影响其他实例

        console.log(stu.pets)
        console.log(stu2.pets)
```

3，多态

允许将子类类型的[指针](https://baike.baidu.com/item/%E6%8C%87%E9%92%88/2878304)赋值给父类类型的指针 

五大原则：

1，单一职责原则

2，开放封闭原则

3，里式替换原则

4，依赖倒置原则

5，接口分离原则