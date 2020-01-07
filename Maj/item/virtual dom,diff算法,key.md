1.virtual dom  https://segmentfault.com/a/1190000008782928?utm_source=tag-newest
virtual dom 通俗易懂的来说就是用一个简单的对象去代替复杂的dom对象

很多时候手工优化dom确实比virtual dom效率高，对于比较简单的dom结构纯手工优化没问题，但是当页面结构很庞大，结构很复杂，手工优化会花去大量时间，而且维护性不高
，不能保证每个人都有手动优化的能力。至此，virtual dom应运而生，virtual dom很多时候都不是最优化的，但是它具有普适性，在效率、可维护之间达到平衡。virtual dom
的另一个重大的意义就是提供一个中间层，js去写ui，ios安卓之类的负责渲染，就像reactNative一样。


2.vue就地复用 https://www.zhihu.com/question/61078310/answer/361261031
就地复用模式是高效的，但是只适用于不依赖子组件状态或者临时dom状态（表单输入值）的列表渲染输出

3.diff算法  https://segmentfault.com/a/1190000008782928?utm_source=tag-newest
Diff 的出现，就会为了减少更新量，找到最小差异部分DOM，只更新差异部分DOM就好了这样消耗就会小一些，数据变化一下，没必要把其他没有涉及的没有变化的DOM 也替换了
(vue react 的diff ?)比较只会在同级比较，不会跨层级比较

4.key的作用 https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/1
key是给每一个vnode的唯一id,可以依靠key,更准确, 更快的拿到oldVnode中对应的vnode节点。
