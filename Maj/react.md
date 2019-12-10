

##### react单项数据流与vue双向数据流有什么区别？

##### 如何理解虚拟dom

##### React Hook原理

##### react16 fiber？



##### 列表diff中key的作用？

**setstate是异步还是同步**

##### React在什么情况下会render？

初始化

一个组件调用了setState()函数时，不论state是否发生了变化，该组件都将被重新渲染。

只要父组件重新渲染了，那么子组件就会重新渲染

但是有些时候我们更新了某个组件的数据，但是并不想让与其相关的其他组件被重渲染，因为反复的重渲染未变化的组件，既耗时也会影响性能，此时就需要对React的重渲染进行优化，shouldComponentUpdate(nextProps,nextState )是重渲染时render函数调用之前被调用的函数，它接收两个参数：nextProps和nextState，分别表示下一个props和下一个state的值，并且，当函数返回false时，阻止接下来的render()函数的调用，阻止组件重渲染，而返回true时，组件照常重渲染，React默认返回true。

##### 什么是受控组件与非受控组件？

react官方推荐使用受控组件来**实现表单**，在受控组件中，表单数据由 React 组件处理。如果让表单数据由 DOM 处理时，替代方案为使用非受控组件。 

受控组件有两个特点：

1. 设置value值，value由state控制，
2. value值一般在**onChange**事件中通过setState进行修改 。

非受控组件有两个特点：

1. 不设置value值，
2. 通过ref获取dom节点然后再取value值 

##### 什么是状态提升？

使用 react 经常会遇到几个组件需要共用状态数据的情况。这种情况下，我们最好将这部分共享的状态提升至他们最近的父组件当中进行管理 

##### 什么是高阶组件？

高阶组件就是一个函数，且该函数接受一个组件作为参数，并返回一个新的组件。

```js
import React, { Component } from 'react';
export default (WrappedComponent) => {
  return class InputHOC extends Component {
    constructor(props) {
      super(props);
      this.state = {
        value: '',
      }
    }
    handleChange = (e) => {
      this.setState({
        value: e.target.value,
      });
    }
    render() {
      const passProps = {
        value: this.state.value,
        onChange: this.handleChange,
      }
      return <WrappedComponent {...passProps} />;
    }
  }
}
//
import React, { Component } from 'react';
import InputHOC from './InputHOC';
class Input extends Component {
  render() {
    return (
      <input className="input" type="text" {...this.props} />
    )
  }
}
export default InputHOC(Input);
```



##### 什么是上下文context？

Context 通过组件树提供了一个传递数据的方法，从而避免了在每一个层级手动的传递 props 属性 

##### 为什么列表循环渲染的key最好不要用index ？

```js
变化前数组的值是[1,2,3,4]，key就是对应的下标：0，1，2，3
变化后数组的值是[4,3,2,1]，key对应的下标也是：0，1，2，3
//那么diff算法在变化前的数组找到key =0的值是1，在变化后数组里找到的key=0的值是4
//因为子元素不一样就重新删除并更新
//但是如果加了唯一的key,如下
变化前数组的值是[1,2,3,4]，key就是对应的下标：id0，id1，id2，id3
变化后数组的值是[4,3,2,1]，key对应的下标也是：id3，id2，id1，id0
//那么diff算法在变化前的数组找到key =id0的值是1，在变化后数组里找到的key=id0的值也是1
//因为子元素相同，就不删除并更新，只做   移动操作   ，这就提升了性能

说到底，key的作用就是更新组件时判断两个节点是否相同。相同就复用，不相同就删除旧的创建新的。在渲染简单的无状态组件时，如果不添加key组件默认都是就地复用，不会删除添加节点，只是改变列表项中的文本值，要知道节点操作是十分耗费性能的。而添加了key之后，当对比内容不一致时，就会认为是两个节点，会先删除掉旧节点，然后添加新节点。
```

##### 简单谈一下react的事件机制？



##### 为什么react不嫩更直接更改state而Vue可以？

##### Vue和react的数据流分别是?

**vue,react区别**









