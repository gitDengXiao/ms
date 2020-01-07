```js
下面是grid简单的概念（阮一峰 http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html，掘金https://juejin.im/post/5c997ab05188252d6534581e#comment）
Flexbox属于一维布局
Grid Layout 二维布局模型，所谓的一维就是只有行，而所谓的二维就是有行也有列。
容器 container   项目item   单元格 cell  网格线   
Grid布局属性分为两类。一类是在容器上的，成为容器属性，另一类是在项目上的，叫做项目属性
容器属性：：：：
1，display grid、inline-grid   注意设置为网格布局后，容器子元素（项目）的float，inline-block，verticval-align等将会失效
2，grid-template-rows属性定义每一列的宽度，grid-template-columns定义每一行的高度
	2.1,repeat(),重复写同样的值非常麻烦，尤其网格很多时。这个时候可以使用repeat（）函数。
	2.2,auto-fill,自动填充
	2.3,fr(fraction 片段)。如果两列的宽度是1fr 和 2fr ，表示后者是前者的两倍
	2.4,minmax(),长度范围
	2.5,auto,浏览器自己决定长度
3，grid-row-gap 行间距，grid-column-gap列间距，grid-gap属性是grid-row-gap和grid-column-gap的简写(最新标准，grid-前缀可以去掉)
4，grid-template-areas，网格布局允许指定区域（没懂），
5，grid-auto-flow，默认是row，即先行后列，也可以设置为column，变成先列后行
6，justify-items设置单元格水平位置（左中右），align-items属性设置单元格内容垂直位置（上中下），place-item是两个简写
7，justify-content属性是整个内容区容器里面的水平位置
8，grid-auto-rows，grid-auto-column
项目属性：：：：
1，grid-column-start,grid-column-end,grid-row-start,grid-row-end,指定项目的位置，分别定位在哪根网格线
2，grid-column属性是grid-column-start和grid-column-end的合并简写形式，grid-row属性是grid-row-start属性和grid-row-end的合并简写形式。 
3，justify-self属性设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目。
```

