# Vue 实例

一个 Vue 应用由一个通过 `new Vue` 创建的**根 Vue 实例**，以及可选的嵌套的、可复用的组件树组成。

所有的 Vue 组件都是 Vue 实例，并且接受相同的选项对象 (一些根实例特有的选项除外)。





## 数据与方法

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的 property 加入到 Vue 的**响应式系统**中。当这些 property 的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。



当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时就已经存在于 `data` 中的 property 才是**响应式**的。

## 生命周期



**vue 生命周期的作用是什么？第一次页面加载会触发哪几个钩子**？

每个 Vue 实例在被创建时都要经过一系列的初始化过程。在这个过程中也会运行一些叫做**生命周期钩子**的函数，这给了用户在不同阶段添加自己的代码的机会。在控制整个 Vue 实例的过程时更容易形成好的逻辑。

所有的生命周期钩子自动绑定 `this` 上下文到实例中，因此可以访问数据，对 property 和方法进行运算。这意味着**不能使用箭头函数来定义一个生命周期方法** (例如 `created: () => this.fetchTodos()`)。因为箭头函数绑定了父上下文，`this.fetchTodos` 的行为未定义。

生命周期钩子总共分为 8 个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

- beforeCreate：vue 实例的挂载元素 el 还没有。
- created
- beforeMount：vue 实例的 $el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点，data.message 还未替换。
- mounted：vue 实例挂载完成，data.message 成功渲染。
- beforeUpdate：当 data 变化时，会触发 beforeUpdate 和 updated 方法。
- update
- beforeDestory：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 的绑定，但是 dom 结构依然存在。
- destoryed
- activited
- deactivated



> 接口请求一般放在 mounted 中，但需要注意的是服务端渲染时不支持 mounted，需要放到 created 中。



第一次页面加载时会触发 beforeCreate， created， beforeMount， mounted 这几个钩子。



> [Vue 官方API - 生命周期钩子](https://cn.vuejs.org/v2/api/#%E9%80%89%E9%A1%B9-%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E9%92%A9%E5%AD%90)

```html
<div id="app">
	{{msg}}
</div>
<script type="text/javascript">
var vm = new Vue({
	el : "#app",
	data : {
		msg : "hi vue",
	},
	//在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
	beforeCreate:function(){
		console.log('beforeCreate');
	},
	/* 在实例创建完成后被立即调用。
	在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。
	然而，挂载阶段还没开始，$el 属性目前不可见。 */
	created	:function(){
		console.log('created');
	},
	//在挂载开始之前被调用：相关的渲染函数首次被调用
	beforeMount : function(){
		console.log('beforeMount');

	},
	//el 被新创建的 vm.$el 替换, 挂在成功	
	mounted : function(){
		console.log('mounted');
	
	},
	//数据更新时调用
	beforeUpdate : function(){
		console.log('beforeUpdate');
			
	},
	//组件 DOM 已经更新, 组件更新完毕 
	updated : function(){
		console.log('updated');
			
	}
});
setTimeout(function(){
	vm.msg = "change ......";
}, 3000);
</script>
```

绿色方框：内部做的事情

红色方框：钩子函数


<div align="center"> <img src="pics/前端 - Vue lifecycle.png"/> </div><br>





# 参考资料