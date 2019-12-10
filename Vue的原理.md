Vue的原理

input和change事件的区别

- input触发条件：输入框字符发生变化
- change触发条件：输入框失去焦点
- v-model的原理
  - 本质上是语法糖
    - 属性绑定和事件绑定
    - 默认事件是input
    - 可以使用lazy修饰符转化change事件

```
<input type="text" v-model='uname'>
<input type="text" v-model.lazy='uname'>
<input type="text" :value='uname' @input='handle'>
```

------

- 双向绑定原理：defineProperty
  - set
  - get
- Vue内部会把data中的数据通过defineProperty方法转化为set和get的监控方式
- 当data中的数据发生变化时，会触发对应的set或者get
  - 修改属性值的时候，触发set方法
  - 访问属性值的时候，触发get方法
- 监控数据变化的目的还是为了更新页面（仅仅更新数据变化对应的DOM节点：尽可能少的更新DOM）
- 完成上述要求需要底层虚拟DOM的支持
- 如何理解虚拟DOM？
- 虚拟DOM是对真实DOM的一种描述

```
VNODE 虚拟节点：描述了真实的DOM节点，本质上就是普通对象
{
	tagName: 'div'
	attrs: { class: "active", id: "info"}
	content: "hello"
}
```

- 虚拟DOM也会形成一个树状结构，描述了真实的DOM树
- 如果数据发生变化，那么就会触发虚拟DOM数的对比（diff算法）
- 对比的结果是：有变化的虚拟节点的集合
- 上述虚拟节点需要转化为真实的DOM节点

```
var div = document.createElement(vnode.tagName)
div.setAttibute(key, value)
div.innerHTML = vnode.content
```

- 最终会把真实的节点更新到页面

------

- 双向数据绑定和虚拟DOM
  - DOM的更新比较耗时
  - 尽可能少的更新DOM节点
  - 为了实现上述需求，发明了虚拟DOM
  - 虚拟DOM描述了真实DOM（虚拟DOM树---真实DOM树）
    - 虚拟DOM树本质其实就是普通对象
  - 当数据发生变化时，会对比变化前后的虚拟DOM树（diff算法）
  - 对比的结果：有变化的虚拟节点的集合
  - 虚拟的节点需要转化成真实DOM节点
  - 把真实的DOM节点渲染到页面

