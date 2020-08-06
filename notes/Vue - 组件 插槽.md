# 插槽



Vue 实现了一套内容分发的 API，这套 API 的设计灵感源自 [Web Components 规范草案](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md)，将 `<slot>` 元素作为承载分发内容的出口。

slot（插槽），目的是让我们封装的组件更加具有扩展性。让使用者可以决定组件内部的一些内容到底展示什么。



## 具名插槽

> 自 2.6.0 起有所更新。已废弃的使用 `slot` attribute 的语法在[这里](https://cn.vuejs.org/v2/guide/components-slots.html#废弃了的语法)。

当子组件的功能复杂时，子组件的插槽可能并非只有一个，如何区分插入的是哪一个？这时候，需要给插槽起一个名字。

```html
<!-- 父组件模板 -->
<div id="app">
    <cpn><span>标题</span></cpn>
    <cpn><button>标题</button></cpn>
</div>
<!-- 子组件模板 -->
<template id="cpn">
    <div>
        <slot><span>左边</span></slot>
        <slot><span>中间</span></slot>
        <slot><span>右边</span></slot>
    </div>
</template>
```

结果：

- 标题 标题 标题 标题
- <button slot="left">标题</button> <button slot="left">标题</button> <button slot="left">标题</button> <button slot="left">标题</button>



**基本使用**

在子组件模板中，给插槽添加 `name` 属性。

```html
<template id="cpn">
    <div>
        <slot name="left"><span>左边</span></slot>
        <slot name="center"><span>中间</span></slot>
        <slot name="right"><span>右边</span></slot>
        <slot>哈哈哈</slot>
    </div>
</template>
```

在父组件模板中，在子组件标签内添加替换元素。给替换元素添加 `slot` 属性，指定使用的插槽，属性值和 `name` 属性值对应 。

```html
<div id="app">
    <cpn><span>标题</span></cpn>
    <cpn><span slot="center">标题</span></cpn>
    <cpn><button slot="left">标题</button></cpn>
</div>
```

结果：

- 左边 中间 右边 标题
- 左边 标题 右边 哈哈哈
- <button slot="left">标题</button> 中间 右边 哈哈哈



## 编译作用域

父组件模板的所有东西都会在父级作用域内编译；子组件模板的所有东西都会在子级作用域内编译。



## 作用域插槽

总结：父组件替换插槽的标签，但是内容由子组件来提供。





















