

##### Vue(mvvm)钩子函数

服务端渲染期间不执行的钩子函数：所有的生命周期钩子函数中，只有 beforeCreate 和 created 会在服务器端渲染(SSR)过程中被调用。这就是说任何其他生命周期钩子函数中的代码（例如 beforeMount 或 mounted），只会在客户端执行。 

2.5.0 新增 errorCaptured 捕获一个来自子孙组件的错误时被调用 ,此钩子可以返回false以阻止该错误继续向上传播。 

##### Vue双向绑定原理

数据劫持：Vue采用 **数据劫持** 结合 **发布者-订阅模式**，通过Object.defineProperty()来劫持各个属性的getter,setter,在数据变动时候发布消息给订阅者，触发相应的回调。

具体为以下几点：

1、实现一个数据监听器observer，能够对数据对象所有属性进行监听，如有变动可拿到最新值并通知订阅者。

2、实现一个指令解析器compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定响应的更新函数。

3、实现一个watcher，作为连接observer和compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的响应回调函数，从而更新视图。

##### vue scoped 原理

##### Vue 组件 data 为什么必须是函数 

每个组件都是 Vue 的实例 

组件共享 data 属性，当 data 的值是同一个引用类型的值时，改变其中一个会影响其他 

##### Vue computed实现，与watch比较

计算属性的主要场景是代替模板内的表达式，或者data值得任何复杂逻辑都应该使用computed来计算它的优势：

1.逻辑清晰，便于管理

2.计算值会被缓存，依赖的data值改变时才会从新计算

**相同**： computed和watch都起到监听/依赖一个数据，并进行处理的作用 

**异同**：它们其实都是vue对监听器的实现，只不过**computed主要用于对同步数据的处理，watch则主要用于观测某个值的变化去完成一段开销较大的复杂业务逻辑**。能用computed的时候优先用computed，避免了多个数据影响其中某个数据时多次调用watch的尴尬情况。

##### vue定时器问题

方案一常规操作定义timer在beforeDestroy销毁

方案二通过$once这个事件侦听器器在定义完定时器之后的位置来清除定时器。 

```js
const timer = setInterval(() =>{                    
    // 某些定时器操作                
}, 500);            
// 通过$once来监听定时器，在beforeDestroy钩子可以被清除。
this.$once('hook:beforeDestroy', () => {            
    clearInterval(timer);                                    
})
```

##### vue 通信

复杂应用：vuex

父向子  ： props   ，$children

子向父   :   emit    $parent

跨组件： provide/inject ，Vue2.2.0新增API,这对选项需要一起使用，**以允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在起上下游关系成立的时间里始终生效**。一言而蔽之：祖先组件中通过provider来提供变量，然后在子孙组件中通过inject来注入变量。 **provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系**。

非父子组件、兄弟组价：

中央事件总线

$on方法用来监听一个事件

$emit用来触发一个事件

##### ref,refs,slot,slots

**ref**：被用来给元素或子组件注册引用信息，引用信息将会注册在父组件的$refs对象上。如果在普通的DOM元素上使用，那么指向的就是普通的DOM元素。 

1、ref 加在普通的元素上，用this.ref.name 获取到的是dom元素 

2、ref 加在子组件上，用this.ref.name 获取到的是组件实例，可以使用组件的所有方法。 

