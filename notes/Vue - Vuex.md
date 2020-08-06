

# 概述

**Vuex 是什么？**

Vuex 是一 个专为 Vue js 应用程序开发的**状态管理模式**。

- 它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。
- Vuex 也集成到 Vue 的官方调试工具 devtools extension，提供了诸如零配置的 time -travel 调试、状态快照导入导出等高级调试功能。



可以将“状态管理”看成把需要多个组件共享的变量全部存储在一个对象里面。

vuex 提供了一个在多个组件间共享状态的插件。虽然自己封装也能实现，但是比较麻烦，而且vuex 可以保证其属性是响应式的。



有什么状态需要在多个组件间共享的呢？

比如用户的登录状态、用户名称、头像、地理位置信息等等。比如商品的收藏、购物车中的物品等等。

这些状态信息，我们都可以放在统一的地方，对它进行保存和管理，而且它们还是响应式的。



单个组件中进行状态管理：

![image-20200801222759749](G:\Offer\DIY-总结\Front end-Offer-Notes（本地文件版）\notes\pics\image-20200801222759749.png)





```
npm install vuex --save
```



<div align="center"> <img src="pics/state.png"/> </div><br>

vuex 是针对 Vue.js 框架实现的状态管理系统。

为了使用 vuex，要引入 store ，并注入 Vue.js 组件中，在组件内部即可通过 $store 访问 store 对象。

使用场景包括：在单页应用中，用于组件之间的通信，例如音乐播放、登录状态管理、加入购物车等。





Vuex有几个比较核心的概念:

- State：共享状态
- Getters
- Mutation：方法
- Action ：异步操作
- Module：模块



State 单一状态树

Vuex 提出使用单一状态树（Single Source of Truth，单一数据源）管理应用层级的全部状态。

单一状态树能够让我们最直接的方式找到某个状态的片段，而且在之后的维护和调试过程中，也可以非常方便的管理和维护。





Vuex的store状态的更新唯一方式:提交Mutation



Mutation主要包括两部分:

- 字符串的事件类型( type )
- 一个回调函数( handler ) ,该回调函数的第一个参数就是state.



**传递参数**

在通过 mutation 更新数据的时候,有可能我们希望携带一 些额外的参数

参数被称为是 mutation 的载荷(Payload)



**提交风格**





vuex 的响应式原理

Vuex 的 store 中的 state 是响应式的，当 state 中的数据发生改变时，Vue组件会自动更新。

这就要求我们必须遵守一些 Vuex 对应的规则：

- 提前在 store 中初始化好所需的属性。
- 当给 state 中的对象添加新属性时，使用下面的方式:
  - 方式一：使用 Vue.set(obj, 'newProp', 123)
  - 方式二：用新对象给旧对象重新赋值



state属性会被添加到响应式系统，而响应式系统会监听属性的变化。当属性发生变化时，会通知所有界面中用到该属性的地方，让界面发生刷新。



mutations常量类型



通常情况下, Vuex要求我们Mutation中的方法必须是同步方法.
0主要的原因是当我们使用devtools时,可以devtools可以帮助我们捕捉mutation的快照.



Action类似于Mutation,但是是用来代替Mutation进行异步操作的.



Vue使用单一状态树,那么也意味着很多状态都会交给Vuex来管理.

当应用变得非常复杂时,store对象就有可能变得相当臃肿.

为了解决这个问题, Vuex允许我们将store分割成模块(Module),而每个模块拥有自己的state、mutations，action、getters等





















