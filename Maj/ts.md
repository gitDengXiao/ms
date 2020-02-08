vue+ts admin   https://armour.github.io/vue-typescript-admin-docs/zh/guide/> 

阮一峰  <https://ts.xcatliu.com/introduction/what-is-typescript> 



笔记

1，声明一个 `void` 类型的变量没有什么用，因为你只能将它赋值为 `undefined` 和 `null`，但是strit模式，null报错

2，如果变量在未声明之前，未指定其类型，那么他会识别为任意类型，等价位 something:any

3，类型推论

4，联合类型，另外，当 TypeScript 不确定一个联合类型的变量到底是哪个类型的时候 ，只能访问联合类型的所有类型共有的属性或方法

5，对象的类型--接口

在typescript中，我们使用接口（interface）来定义对象的类型

6，函数

```
注意不要混淆了 TypeScript 中的 => 和 ES6 中的 =>。
在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```

7，类型断言

8，声明文件(不懂)

9，类型别名(不懂)

10，字符串字面类型（不懂）

类型别名与字符串字面类型都是使用type进行定义

11，元祖

数组合并了相同类型的对象，而元组（Tuple）合并了不同类型的对象。 

```ts
let tom: [string, number] = ['Tom', 25];
```

12，枚举（Enum）类型用于取值被限定在一定范围内的场景 

13，类

14，类与接口

15，泛型

泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。 