



# 模板语法

## 插值语法

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML，所以能被遵循规范的浏览器和 HTML 解析器解析。

在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。





### Mustache 语法

> Mustache：胡子/胡须

数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```html
<span>Message: {{ msg }}</span>
```

Mustache 标签将会被替代为对应数据对象上 `msg` property 的值。无论何时，绑定的数据对象上 `msg` property 发生了改变，插值处的内容都会更新。

mustache 语法中，不仅仅可以直接写变量，还可以写简单的表达式

```html
<h2>{{firstName + lastName}}</h2>
<h2>{{firstName + ' ' + lastName}}</h2>
<h2>{{firstName}} {{lastName}}</h2>
<h2>{{counter * 2}}</h2>
```



### `v-once` 指令

通过使用 [v-once 指令](https://cn.vuejs.org/v2/api/#v-once) 能执行一次性地插值，当数据改变时，插值处的内容不会更新。但这会影响到该节点上的其它数据绑定：

```html
<span v-once>这个将不会改变: {{ msg }}</span>
```



### `v-html` 指令

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，需要使用 [`v-html` 指令](https://cn.vuejs.org/v2/api/#v-html)：

```html
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

站点上动态渲染的任意 HTML 可能会非常危险，因为很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，**绝不要**对用户提供的内容使用插值。



### `v-text` 指令

```html
<h2 v-text="message"></h2>	
```

v-text 不灵活，会覆盖掉元素的内容

```html
<h2>{{message}}，李银河</h2>
<h2 v-text="message">，李银河</h2>	
<!-- v-text 只显示 message 包含的数据 -->
```



### `v-pre` 指令

原封不动的解析

```html
<h2 v-pre>{{message}}</h2>
```



### `v-cloak` 指令

cloak，“斗篷，遮盖物”

在 Vue 实例解析之前，`div` 元素有 vue-cloak 属性，解析之后，`div`  没有 vue-cloak 属性。

```html
<div id="app" v-cloak>{{message}}</div>
```

```html
<style>
    [v-cloak]{
        background-color: green;
    }
</style>
```



**Attribute**

Mustache 语法不能作用在 HTML attribute 上，遇到这种情况应该使用 [`v-bind` 指令](https://cn.vuejs.org/v2/api/#v-bind)：

```html
<div v-bind:id="dynamicId"></div>
```

对于布尔 attribute (它们只要存在就意味着值为 `true`)，`v-bind` 工作起来略有不同，在这个例子中：

```html
<button v-bind:disabled="isButtonDisabled">Button</button>
```

如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` attribute 甚至不会被包含在渲染出来的 `<button>` 元素中。



**使用 JavaScript 表达式**

对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。

```html
{{ number + 1 }}
{{ ok ? 'YES' : 'NO' }}
{{ message.split('').reverse().join('') }}
<div v-bind:id="'list-' + id"></div>
```

每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```html
<!-- 这是语句，不是表达式 -->
{{ var a = 1 }}

<!-- 流控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```

模板表达式都被放在沙盒中，只能访问[全局变量的一个白名单](https://github.com/vuejs/vue/blob/v2.6.10/src/core/instance/proxy.js#L9)，如 `Math` 和 `Date` 。你不应该在模板表达式中试图访问用户定义的全局变量。



## `v-bind` 指令

`v-bind` 用于绑定一个或多个属性值，或者向另一个组件传递 props。



### 绑定基本属性

除了内容需要动态来决定外，某些属性我们也希望动态来绑定。`v-bind` 指令可以用于响应式地更新 HTML 属性。

下面的例子中， `v-bind` 指令将该元素的 `src` 属性与表达式 `imgURL` 的值绑定，`href` 属性与表达式 `link` 的值绑定。

```html
<img v-bind:src="imgURL" alt="">
<a v-bind:href="link">百度一下</a>
```

```js
const app = new Vue({
    el: '#app',
    data: {
        imgURL: "http://p1.music.126.net/DDbWooTaERVWr4Bw2D3tbQ==/109951165176545416.jpg?imageView&quality=89",
        link: "http://www.baidu.com"
    }
})
```

`v-bind` 的语法糖（简写/缩写形式）， `v-bind:` 用 `:` 代替。

```html
<a :href="link">百度一下</a>
```



### **绑定 HTML Class**

操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是 attribute，所以可以用 `v-bind` 处理它们：只需要通过表达式计算出字符串结果即可。不过，字符串拼接麻烦且易错。因此，在将 `v-bind` 用于 `class` 和 `style` 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。

绑定 Class 有两种方式：

- 对象语法
- 数组语法，用得比较少

应用：

点击列表中不同项时，样式转变



#### 对象语法

可以传给 `v-bind:class` 一个对象，以动态地切换 class。



有下面四种用法：

- 直接通过 { } 绑定一个 class。

```html
<h2 :class="{active: true, line: false}">active1</h2>
```

- 通过判断布尔值，传入更多字段来动态切换多个 class。
- 可以和普通的 class 属性同时存在，并不冲突。

```html
<h2 class="title" :class="{active: isActive,line: isLine}">active2</h2>
```

 data：

```js
data: {
  isActive: true,
  isLine: false
}
```

当 `isActive` 或者 `isLine` 变化时，class 列表将相应地更新。

- 绑定的数据对象不必内联定义在模板里。可以放在 data 中。如果过于复杂，可以放在一个 methods 或者 computed 中。

**作为一个对象放在 data 里：**

```html
<div :class="classObject"></div>
data: {
  classObject: {
    active: true,
    line: false
  }
}
```

**作为一个函数放在 methods 里：**

```html
<h2 class="title" :class="getClasses()">{{message}}</h2>
<button v-on:click="btnClink">按钮</button>
```

在 methods 中声明 getClass 方法动态绑定 class，声明 btnClink 可以通过按钮控制 class。

```js
methods: {
    btnClink: function(){
        this.isActive = !this.isActive;
    },
        getClasses: function(){
            return {active: this.isActive,line: this.isLine}
        }
}
```

**放在 computed里面：**

```html
<div v-bind:class="classObject"></div>
```

data 和 computed

```js
data: {
  isActive: true,
  error: null
},
computed: {
  classObject: function () {
    return {
      active: this.isActive && !this.error,
      'text-danger': this.error && this.error.type === 'fatal'
    }
  }
}
```





#### 数组语法

我们可以把一个数组传给 `v-bind:class`，以应用一个 class 列表。

在 [ ] 里面加上单引号，会当做字符串处理。下面两个标签的 class 相同。

```html
<h2 class="title active line">{{message}}</h2>
<h2 class="title" :class="['active','line']">{{message}}</h2>
```



将 [ ] 里面的变量放在 data 或 methods 中。两个标签的 class 都是 title aaa bbb。

```html
<h2 class="title" :class="[active,line]">你好！</h2>
<h2 class="title" :class="getClasses()">你好！</h2>
```

data 和 methods：

```js
data: {
	active: 'aaa',
    line: 'bbb'
},
methods: {
	getClasses: function (){
		return [this.active, this.line]
	}
}
```

渲染为：

```html
<h2 class="title aaa bbb"></h2>
```



根据条件切换列表中的 class，可以用三元表达式：

```html
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
```

这样写将始终添加 `errorClass`，但是只有在 `isActive` 是 truthy[[1\]](https://cn.vuejs.org/v2/guide/class-and-style.html#footnote-1) 时才添加 `activeClass`。

不过，当有多个条件 class 时这样写有些繁琐。所以在数组语法中也可以使用对象语法：

```html
<div v-bind:class="[{ active: isActive }, errorClass]"></div>
```





#### 用在组件上

当在一个自定义组件上使用 `class` property 时，这些 class 将被添加到该组件的根元素上面。这个元素上已经存在的 class 不会被覆盖。

例如，如果你声明了这个组件：

```html
Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})
```

然后在使用它的时候添加一些 class：

```html
<my-component class="baz boo"></my-component>
```

HTML 将被渲染为：

```html
<p class="foo bar baz boo">Hi</p>
```

对于带数据绑定 class 也同样适用：

```html
<my-component v-bind:class="{ active: isActive }"></my-component>
```

当 `isActive` 为 truthy （转换后的值为真的值）时，HTML 将被渲染成为：

```html
<p class="foo bar active">Hi</p>
```





### 绑定内联样式

绑定 Style 有两种方式：

- 对象语法
- 数组语法

应用：

在组件中，元素的样式不能“写死”





对象语法

style 后面跟一个对象。对象的 key 是CSS 属性名称，value 是属性值（值可以是data中的属性）

```
<h2 :style="{key(属性名):value(属性值)}">{{message}}</h2>
```

数组语法

style 后面跟一个数组类型，多个值以逗号分割即可。



#### 对象语法

`v-bind:style` 的对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，需要用引号括起来) 来命名：

```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
```

属性值需要加引号，不然会解析成变量。

```js
data: {
  activeColor: 'red',		// 需要加引号
  fontSize: 30
}
```



可以直接绑定到 data 中作为一个样式对象，这会让模板更清晰。也可以在 methods 中声明。

```html
<h2 :style="styleObject">styleObject</h2>
<h2 :style="getStyles()">getStyles</h2>
```

data 和 methods ：

```js
data: {
    message: '你好！',
	styleObject: {
		finalSize: '50px',
		finalColor: 'red',
	}
},
methods: {
	getStyles: function() {
    	return {fontSize:this.finalSize + 'px',color: this.finalColor}
    }
}
```

同样的，对象语法常常结合返回对象的计算属性使用。



#### 数组语法

`v-bind:style` 的数组语法可以将多个样式对象应用到同一个元素上：

```html
<h2 :style="[baseStyles,overridingStyles]">{{message}}</h2>
```

```js
data: {
    message: '你好！',
    baseStyles: {backgroundColor:'red'},
    overridingStyles: {color: 'white'}
}
```



#### 自动添加前缀

当 `v-bind:style` 使用需要添加[浏览器引擎前缀](https://developer.mozilla.org/zh-CN/docs/Glossary/Vendor_Prefix)的 CSS property 时，如 `transform`，Vue.js 会自动侦测并添加相应的前缀。



#### 多重值

> 2.3.0+

从 2.3.0 起可以为 `style` 绑定中的 property 提供一个包含多个值的数组，常用于提供多个带前缀的值，例如：

```html
<div :style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"></div>
```

这样写只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的 flexbox，那么就只会渲染 `display: flex`。



## 计算属性



模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。对于任何复杂逻辑，都应当使用**计算属性**。

### **基础例子**

需要在元素中插入两个值时，有以下三种解决方案。

```html
<div id="app">
    <!-- 1. 直接拼接：过于繁琐 -->
    <h2>{{firstName}} {{lastName}}</h2>
    <h2>{{firstName +' ' + lastName}}</h2>
    
    <!-- 2. 通过定义methods -->
    <!-- 在双大括号里面放变量，如果放方法会有点别扭 -->
    <h2>{{getFullName()}}</h2>
    
    <!-- 3. 通过computed -->
    <!-- 计算属性，不需要加小括号 -->
    <h2>{{fullName}}</h2>
</div>
```

```js
const app = new Vue({
    el: '#app',
    data: {
        firstName: 'Reborn',
        lastName: 'July'
    },
    methods: {
        getFullName: function(){
            return this.firstName+' '+this.lastName
        }
    },
    // 计算属性
    computed: {
        // 计算属性的 getter
        // 命名时，不像方法需要加上动词。
        fullName: function(){
            // `this` 指向 app
            return this.firstName+' '+this.lastName
        }
    }
})
```

可以像绑定普通 property 一样在模板中绑定计算属性。 `app.fullName` 依赖于 `app.firstName` 和 `app.lastName` ，因此当后面两个值发生改变时，所有依赖 `app.fullName ` 的绑定也会更新。

而且最妙的是以声明的方式创建这种依赖关系：计算属性的 getter 函数是没有副作用的，这使它更易于测试和理解。





### **计算属性的 setter**

计算属性默认只有 getter，不过在需要时也可以提供一个 setter：

```js
// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```

在 console 里面运行 `app.fullName = 'John Doe'` 时，setter 会被调用，`app.firstName` 和 `app.lastName` 也会相应地被更新。

回顾并对比基础例子，总结如下：

- 在元素中调用计算属性时，不需要加小括号。从完整的 `fullName` 写法可以看出 ，`fullName` 是一个包含 getter 和 setter 函数的属性，而不是一个方法。
- 计算属性一般没有 setter 方法，默认只有 getter，作为一个只读属性存在（不能直接修改 `app.fullName`）。因此， `fullName` 可以采取基础例子中的写法，不显示声明 getter。
- 计算属性可以通过响应式依赖改变值。即，通过 data 中的数据影响 computed 中对应的数据。



### **computed vs methods**

我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。

然而，不同的是**计算属性是基于它们的响应式依赖进行缓存的**。只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要计算属性中对应的 data 数据还没有发生改变，多次访问计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 `Date.now()` 不是响应式依赖：

```js
computed: {
  now: function () {
    return Date.now()
  }
}
```

相比之下，每当触发重新渲染时，调用方法将**总会**再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 **A**，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 **A**。如果没有缓存，我们将不可避免的多次执行 **A** 的 getter！如果你不希望有缓存，请用方法来替代。



### **计算属性 vs 侦听属性**



Vue 提供了一种更通用的方式来观察和响应 Vue 实例上的数据变动：**侦听属性**。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 `watch`——特别是如果你之前使用过 AngularJS。然而，通常更好的做法是使用计算属性而不是命令式的 `watch` 回调。细想一下这个例子：

```
<div id="demo">{{ fullName }}</div>
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```

上面代码是命令式且重复的。将它与计算属性的版本进行比较：

```
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```





## `v-on` 事件监听  



 `v-on` 指令，它用于监听 DOM 事件，让用户和应用进行交互。

用法：绑定事件监听器。事件类型由参数指定。表达式可以是一个方法的名字或一个内联语句，如果没有修饰符也可以省略。

用在普通元素上时，只能监听[**原生 DOM 事件**](https://developer.mozilla.org/zh-CN/docs/Web/Events)。用在自定义元素组件上时，也可以监听子组件触发的**自定义事件**。

### **基本使用**

下例实现一个计数器。

```html
<div id="app">
    <h2>当前计数:{{ counter }}</h2>
    <!-- 参数是监听的事件名 click -->
    <button v-on:click="increment">+</button>
    <!-- v-on 的缩写形式 -->
    <button @click="subtraction">-</button>
</div>
```

在 methods 中定义对应的方法：

```js
const app = new Vue({
    el:'#app',
    data: {
        counter:0
    },
    methods:{	
        increment(){
            this.counter++;
        },
        subtraction(){
            this.counter--;
        }
    }
})
```

### 参数

在 View 层 v-on 指令的参数是监听的事件名。

事件调用的方法的参数有以下情况：

- 如果该方法不需要额外参数，那么在调用该方法时，后面的小括号可以不添加。比如，`@click="btn3Click"`。
- 如果方法需要参数，方法后面有小括号但是没有传入参数，会将方法的形参以 undefined 处理。比如，`@click="btn3Click()"`。
- 如果方法需要参数，方法后面没有小括号，默认将浏览器生成的event 事件对象传入到方法中。
- 如果需要 event 对象，同时又需要其它参数，可以通过 `$event` 传入方法。比如：`@click="btn3Click(123,$event)"`。



### 修饰符

- `.stop` - 调用 `event.stopPropagation()`，阻止冒泡。
- `.prevent` - 调用 `event.preventDefault()`。
- `.capture` - 添加事件侦听器时使用 capture 模式。
- `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
- `.{keyCode | keyAlias}` - 只当事件是从特定键触发时才触发回调。比如：`@keyup.enter="keyup"`。
- `.native` - 监听组件根元素的原生事件。
- `.once` - 只触发一次回调。
- `.left` - (2.2.0) 只当点击鼠标左键时触发。
- `.right` - (2.2.0) 只当点击鼠标右键时触发。
- `.middle` - (2.2.0) 只当点击鼠标中键时触发。
- `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器





同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：

```
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`。



## 条件渲染

### `v-if` 

`v-if` 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。

#### **在 `<template>` 元素上使用 v-if 条件渲染分组**

因为 `v-if` 是一个指令，所以必须将它添加到一个元素上。如果想切换多个元素，可以把一个 `<template>` 元素当做不可见的包裹元素，并在上面使用 `v-if`。最终的渲染结果将不包含 `<template>` 元素。

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

#### **`v-else`**

可以使用 `v-else` 指令来表示 `v-if` 的“else 块”。`v-else` 元素必须紧跟在带 `v-if` 或者 `v-else-if` 的元素的后面，否则它将不会被识别。

```html
<div v-if="Math.random() > 0.5">
  Now you see me
</div>
<!-- v-else 不用加条件 -->
<div v-else>
  Now you don't
</div>
```

#### **`v-else-if`**

> 2.1.0 新增

`v-else-if`，充当 `v-if` 的“else-if 块”，可以连续使用。类似于 `v-else`，`v-else-if` 也必须紧跟在带 `v-if` 或者 `v-else-if` 的元素之后。

```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```

#### **用 `key` 管理可复用的元素**

Vue 在进行 DOM 渲染时，为了尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。这么做除了使 Vue 变得非常快之外，还有其它一些好处。（更多信息请看 Virtual DOM 原理）

例如，如果允许用户在不同的登录方式（用户名登录和邮箱登录）之间切换：

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>
```

那么在上面的代码中切换 `loginType` 将<u>不会清除用户已经输入的内容</u>。因为两个模板使用了相同的元素，`<input>` 不会被替换掉——仅仅是替换了它的 `placeholder`。

**解决方案**

这样也不总是符合实际需求，所以 Vue 提供了一种方式来表达“这两个元素是完全独立的，不要复用它们”。只需添加一个具有唯一值的 `key` attribute 即可：

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

注意，`<label>` 元素仍然会被高效地复用，因为它们没有添加 `key` attribute。



### [`v-show`](https://cn.vuejs.org/v2/guide/conditional.html#v-show)

另一个用于根据条件展示元素的选项是 `v-show` 指令。用法大致一样：

```html
<h1 v-show="ok">Hello!</h1>
```

不同的是带有 `v-show` 的元素始终会被渲染并保留在 DOM 中。`v-show` 只是简单地切换元素的 CSS 的 `display` 属性。

注意，`v-show` 不支持 `<template>` 元素，也不支持 `v-else`。



### [`v-if` vs `v-show`](https://cn.vuejs.org/v2/guide/conditional.html#v-if-vs-v-show)

两者都是条件渲染指令。不同之处在于：

**本质**

`v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

在 `v-if` 中，当条件为 true 时，元素才会存在于 HTML 页面中。当条件为 false 时，不会有对应的元素存在 DOM 中。

`v-if` 也是**惰性的**：如果在初始渲染时条件为假，则什么也不做，直到条件第一次变为真时，才会开始渲染条件块。

在 `v-show` 中，不管初始条件是什么，元素总是会被渲染，都会存在于 HTML 页面中，并且只是简单地基于 CSS 进行切换。当条件为 false 时，将元素的 style 属性设置为 `style=display:none`。

**性能及使用选择**

一般来说，`v-if` 有更高的切换开销（因为涉及到 DOM 插入删除），而 `v-show` 有更高的初始渲染开销。

因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

**其它**

`v-show` 不支持 `<template>` 元素，也不支持 `v-else`。 `v-if` 都支持。



### [`v-if` 与 `v-for` 一起使用](https://cn.vuejs.org/v2/guide/conditional.html#v-if-与-v-for-一起使用)



可以。但是**不推荐**同时使用 `v-if` 和 `v-for`。请查阅[风格指南](https://cn.vuejs.org/v2/style-guide/#避免-v-if-和-v-for-用在一起-必要)以获取更多信息。

当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。请查阅[列表渲染指南](https://cn.vuejs.org/v2/guide/list.html#v-for-with-v-if)以获取详细信息。



## 列表渲染

### [ `v-for` 遍历数组](https://cn.vuejs.org/v2/guide/list.html#用-v-for-把一个数组对应为一组元素)

我们可以用 `v-for` 指令基于一个数组来渲染一个列表。`v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组，而 `item` 则是被迭代的数组元素的**别名**。

**基本使用**

```html
<ul id="example-1">
  <li v-for="item in items" :key="item.message">
    {{ item.message }}
  </li>
</ul>
```

```js
var example1 = new Vue({
  el: '#example-1',
  data: {
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

结果：

- Foo
- Bar



**获取索引值**

在 `v-for` 块中，我们可以访问所有父作用域的 property。`v-for` 还支持一个可选的第二个参数，即当前项的索引。

```html
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

```js
var example2 = new Vue({
  el: '#example-2',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```

结果：

- Parent - 0 - Foo
- Parent - 1 - Bar

也可以用 `of` 替代 `in` 作为分隔符，因为它更接近 JavaScript 迭代器的语法：

```
<div v-for="item of items"></div>
```



### [`v-for` 遍历对象](https://cn.vuejs.org/v2/guide/list.html#在-v-for-里使用对象)

也可以用 `v-for` 来遍历一个对象的 property。

**获取 value**

```html
<ul id="v-for-object" class="demo">
  <li v-for="value in object">
    {{ value }}
  </li>
</ul>
```

```js
new Vue({
  el: '#v-for-object',
  data: {
    object: {
      title: 'How to do lists in Vue',
      author: 'Jane Doe',
      publishedAt: '2016-04-10'
    }
  }
})
```

结果：

- How to do lists in Vue
- Jane Doe
- 2016-04-10

**获取 key、value**

也可以提供第二个的参数为 property 名称 (也就是键名)：

```html
<div v-for="(value, name) in object">
  {{ name }}: {{ value }}
</div>
```

**获取 key、value、索引**

还可以用第三个参数作为索引：

```
<div v-for="(value, name, index) in object">
  {{ index }}. {{ name }}: {{ value }}
</div>
```

0. title: How to do lists in Vue

1. author: Jane Doe

2. publishedAt: 2016-04-10

在遍历对象时，会按 `Object.keys()` 的结果遍历，但是**不能**保证它的结果在不同的 JavaScript 引擎下都一致。



### [维护状态](https://cn.vuejs.org/v2/guide/list.html#维护状态)



当 Vue 正在更新使用 `v-for` 渲染的元素列表时，它默认使用“就地更新”的策略。如果数据项的顺序被改变，Vue 将不会移动 DOM 元素来匹配数据项的顺序，而是就地更新每个元素，并且确保它们在每个索引位置正确渲染。这个类似 Vue 1.x 的 `track-by="$index"`。

> 比如：对数组 `arr: ['A','B','C','D','E']` 执行 `arr.splice(2,0'F')` 时，理想的方法是先将数组的后三项整体后移一个位置，然后在 'B' 和 'C' 之间插入 'F'。但实际执行过程是将 'C' 更新为 'F'，将 'D' 更新为 'C'，将 'E' 更新为 'D'，最后插入 'E'。

这个默认的模式是高效的，但是**只适用于不依赖子组件状态或临时 DOM 状态 (例如：表单输入值) 的列表渲染输出**。

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，需要为每项提供一个唯一 `key` attribute：

- 虚拟 DOM 的 Diff 算法就可以正确的识别节点
- 找到正确的位置区插入新的节点。

简言之，key 的作用主要是为了高效的更新虚拟 DOM。

```html
<div v-for="item in items" v-bind:key="item.id">
  <!-- 内容 -->
</div>
```

> key 不要绑定索引，因为在插入前后，索引会发生变化。

建议尽可能在使用 `v-for` 时提供 `key` attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

因为它是 Vue 识别节点的一个通用机制，`key` 并不仅与 `v-for` 特别关联。后面我们将在指南中看到，它还具有其它用途。

不要使用对象或数组之类的非基本类型值作为 `v-for` 的 `key`。请用字符串或数值类型的值。

更多 `key` attribute 的细节用法请移步至 [`key` 的 API 文档](https://cn.vuejs.org/v2/api/#key)。



### [数组更新检测](https://cn.vuejs.org/v2/guide/list.html#数组更新检测)

 `v-for` 主要用于遍历数组。了解“哪些数组是响应式的”是有必要的。

#### [变更方法](https://cn.vuejs.org/v2/guide/list.html#变更方法)

Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

可以打开控制台，然后对前面例子的 `items` 数组尝试调用变更方法。比如 `example1.items.push({ message: 'Baz' })`。

#### [替换数组](https://cn.vuejs.org/v2/guide/list.html#替换数组)

变更方法，顾名思义，会变更调用了这些方法的原始数组。相比之下，也有非变更方法，例如 `filter()`、`concat()` 和 `slice()`。它们不会变更原始数组，而**总是返回一个新数组**。当使用非变更方法时，可以用新数组替换旧数组：

```js
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

你可能认为这将导致 Vue 丢弃现有 DOM 并重新渲染整个列表。幸运的是，事实并非如此。Vue 为了使得 DOM 元素得到最大范围的重用而实现了一些智能的启发式方法，所以用一个含有相同元素的数组去替换原来的数组是非常高效的操作。

#### [注意事项](https://cn.vuejs.org/v2/guide/list.html#注意事项)

由于 JavaScript 的限制，Vue **不能检测**数组和对象的变化。[深入响应式原理](https://cn.vuejs.org/v2/guide/reactivity.html#检测变化的注意事项)中有相关的讨论。

在 JavaScript 中执行 `this.letters[0] = 'bbb'`，视图数据不会更新。

- 解决方案一：`this.letters.splice(0,1,'bbb')`
-  解决方案二：`Vue.set(this.letters,0,'bbb')`。第一个参数是要修改的对象，第二个参数是索引值，第三个参数是修改后的值。





### [显示过滤/排序后的结果](https://cn.vuejs.org/v2/guide/list.html#显示过滤-排序后的结果)

有时，我们想要显示一个数组经过过滤或排序后的版本，而不实际变更或重置原始数据。在这种情况下，可以创建一个计算属性，来返回过滤或排序后的数组。

例如：

```
<li v-for="n in evenNumbers">{{ n }}</li>
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

在计算属性不适用的情况下 (例如，在嵌套 `v-for` 循环中) 你可以使用一个方法：

```
<ul v-for="set in sets">
  <li v-for="n in even(set)">{{ n }}</li>
</ul>
data: {
  sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
},
methods: {
  even: function (numbers) {
    return numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```

### [在 `v-for` 里使用值范围](https://cn.vuejs.org/v2/guide/list.html#在-v-for-里使用值范围)

`v-for` 也可以接受整数。在这种情况下，它会把模板重复对应次数。

```
<div>
  <span v-for="n in 10">{{ n }} </span>
</div>
```

结果：

1 2 3 4 5 6 7 8 9 10

### 在 `<template>` 上使用 `v-for`

类似于 `v-if`，你也可以利用带有 `v-for` 的 `<template>` 来循环渲染一段包含多个元素的内容。比如：

```
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

### [`v-for` 与 `v-if` 一同使用](https://cn.vuejs.org/v2/guide/list.html#v-for-与-v-if-一同使用)

注意我们**不**推荐在同一元素上使用 `v-if` 和 `v-for`。更多细节可查阅[风格指南](https://cn.vuejs.org/v2/style-guide/#避免-v-if-和-v-for-用在一起-必要)。

当它们处于同一节点，`v-for` 的优先级比 `v-if` 更高，这意味着 `v-if` 将分别重复运行于每个 `v-for` 循环中。当你只想为*部分*项渲染节点时，这种优先级的机制会十分有用，如下：

```
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```

上面的代码将只渲染未完成的 todo。

而如果你的目的是有条件地跳过循环的执行，那么可以将 `v-if` 置于外层元素 (或 [`) 上。如：

```
<ul v-if="todos.length">
  <li v-for="todo in todos">
    {{ todo }}
  </li>
</ul>
<p v-else>No todos left!</p>
```

### [在组件上使用 `v-for`](https://cn.vuejs.org/v2/guide/list.html#在组件上使用-v-for)

> 这部分内容假定你已经了解[组件](https://cn.vuejs.org/v2/guide/components.html)相关知识。你也完全可以先跳过它，以后再回来查看。

在自定义组件上，你可以像在任何普通元素上一样使用 `v-for`。

```
<my-component v-for="item in items" :key="item.id"></my-component>
```

> 2.2.0+ 的版本里，当在组件上使用 `v-for` 时，`key` 现在是必须的。

然而，任何数据都不会被自动传递到组件里，因为组件有自己独立的作用域。为了把迭代数据传递到组件里，我们要使用 prop：

```
<my-component
  v-for="(item, index) in items"
  v-bind:item="item"
  v-bind:index="index"
  v-bind:key="item.id"
></my-component>
```

不自动将 `item` 注入到组件里的原因是，这会使得组件与 `v-for` 的运作紧密耦合。明确组件数据的来源能够使组件在其他场合重复使用。

下面是一个简单的 todo 列表的完整例子：

```
<div id="todo-list-example">
  <form v-on:submit.prevent="addNewTodo">
    <label for="new-todo">Add a todo</label>
    <input
      v-model="newTodoText"
      id="new-todo"
      placeholder="E.g. Feed the cat"
    >
    <button>Add</button>
  </form>
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:key="todo.id"
      v-bind:title="todo.title"
      v-on:remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>
```

注意这里的 `is="todo-item"` attribute。这种做法在使用 DOM 模板时是十分必要的，因为在 `<ul>` 元素内只有 `<li>` 元素会被看作有效内容。这样做实现的效果与 `<todo-item>` 相同，但是可以避开一些潜在的浏览器解析错误。查看 [DOM 模板解析说明](https://cn.vuejs.org/v2/guide/components.html#解析-DOM-模板时的注意事项) 来了解更多信息。

```
Vue.component('todo-item', {
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">Remove</button>\
    </li>\
  ',
  props: ['title']
})

new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      {
        id: 1,
        title: 'Do the dishes',
      },
      {
        id: 2,
        title: 'Take out the trash',
      },
      {
        id: 3,
        title: 'Mow the lawn'
      }
    ],
    nextTodoId: 4
  },
  methods: {
    addNewTodo: function () {
      this.todos.push({
        id: this.nextTodoId++,
        title: this.newTodoText
      })
      this.newTodoText = ''
    }
  }
})
```





## `v-model`

### 基本使用



 `v-model` 指令可以在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。

- 修改视图中的数据，data 中的数据也会被修改。
- 通过 console （或源代码）修改 data 中的数据，视图中的数据也会被修改。（Mustache 语法只支持这个绑定，双大括号的内容只能充当元素的内容而不能作为元素的属性值存在）。





### 双向数据绑定原理



 `v-model` 本质上是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。本质上是包含两个操作：

- v-bind 绑定一个 value 属性。
- v-on 指令给当前元素绑定 input 事件。

下面三个 `<input>` 都实现了双向绑定。

```html
<input type="text" v-model="message" />
<input type="text" :value="message" @input="valueChage"/>
<input type="text" :value="message" @input="message = $event.target.value"/>
```

```js
methods: {
	valueChage(event) {
		this.message = event.target.value;
	}
}
```



#### Vue 2.0 原理

Object.defineProperty





#### Vue 3 改进

proxy

 </span>



#### 源码





#### 实现





### 修饰符

- [`.lazy`](https://cn.vuejs.org/v2/guide/forms.html#lazy) - 取代 `input` 监听 `change` 事件

  默认情况下，v-model 在 input 事件中同步输入框中的数据。lazy 修饰符可以让数据只在失去焦点（光标从输入框移到外面）或回车时更新。

- [`.number`](https://cn.vuejs.org/v2/guide/forms.html#number) - 输入字符串转为有效的数字

- [`.trim`](https://cn.vuejs.org/v2/guide/forms.html#trim) - 输入首尾空格过滤







## 指令

指令 (Directives) 是带有 `v-` 前缀的特殊 attribute。指令 attribute 的值预期是**单个 JavaScript 表达式** (`v-for` 是例外情况)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。



**参数**

一些指令能够接收一个“参数”，在指令名称之后以冒号表示。例如，`v-bind` 指令可以用于响应式地更新 HTML attribute：

```html
<a v-bind:href="url">...</a>
```

在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。



**动态参数**

从 2.6.0 开始，可以用方括号括起来的 JavaScript 表达式作为一个指令的参数：

```html
<!--
注意，参数表达式的写法存在一些约束，如之后的“对动态参数表达式的约束”章节所述。
-->
<a v-bind:[attributeName]="url"> ... </a>
```

可以使用动态参数为一个动态的事件名绑定处理函数：

```
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`。

**对动态参数的值的约束**

动态参数预期会求出一个字符串，异常情况下值为 `null`。这个特殊的 `null` 值可以被显性地用于移除绑定。任何其它非字符串类型的值都将会触发一个警告。

**对动态参数表达式的约束**

动态参数表达式有一些语法约束，因为某些字符，如空格和引号，放在 HTML attribute 名里是无效的。例如：

```
<!-- 这会触发一个编译警告 -->
<a v-bind:['foo' + bar]="value"> ... </a>
```

变通的办法是使用没有空格或引号的表达式，或用计算属性替代这种复杂表达式。

在 DOM 中使用模板时 (直接在一个 HTML 文件里撰写模板)，还需要避免使用大写字符来命名键名，因为浏览器会把 attribute 名全部强制转为小写：

```
<!--
在 DOM 中使用模板时这段代码会被转换为 `v-bind:[someattr]`。
除非在实例中有一个名为“someattr”的 property，否则代码不会工作。
-->
<a v-bind:[someAttr]="value"> ... </a>
```



**修饰符**

修饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```
<form v-on:submit.prevent="onSubmit">...</form>
```

在接下来对 [`v-on`](https://cn.vuejs.org/v2/guide/events.html#事件修饰符) 和 [`v-for`](https://cn.vuejs.org/v2/guide/forms.html#修饰符) 等功能的探索中，你会看到修饰符的其它例子。



## **缩写**

`v-` 前缀作为一种视觉提示，用来识别模板中 Vue 特定的 attribute。当你在使用 Vue.js 为现有标签添加动态行为 (dynamic behavior) 时，`v-` 前缀很有帮助，然而，对于一些频繁用到的指令来说，就会感到使用繁琐。同时，在构建由 Vue 管理所有模板的[单页面应用程序 (SPA - single page application)](https://en.wikipedia.org/wiki/Single-page_application) 时，`v-` 前缀也变得没那么重要了。因此，Vue 为 `v-bind` 和 `v-on` 这两个最常用的指令，提供了特定简写：

**`v-bind` 缩写**

```
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
```

**`v-on` 缩写**

```
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

它们看起来可能与普通的 HTML 略有不同，但 `:` 与 `@` 对于 attribute 名来说都是合法字符，在所有支持 Vue 的浏览器都能被正确地解析。而且，它们不会出现在最终渲染的标记中。缩写语法是完全可选的，但随着你更深入地了解它们的作用，你会庆幸拥有它们。
















# 参考资料

