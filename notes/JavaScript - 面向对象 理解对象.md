



# 理解对象

ECMAScript 支持面向对象（OO）编程，但不使用类或者接口。ECMAScript 中没有类的概念，它的对象也与 OOP 语言中的对象不同。

ECMA-262 把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。”，可以 ECMAScript 的对象想象成散列表：一组名值对，其中值可以是数据或函数。

每个对象都是基于一个引用类型创建的，引用类型可以是原生类型，也自定义类型。



创建自定义对象的最简单方式就是使用 new 操作符创建一个 Object 的实例，然后再为它添加属性和方法。

```js
var person = new Object();		// 建了一个名为 person 的对象
// 为 person 添加属性和方法
person.name = "Nicholas";
person.age = 29;
person.sayName = function(){
	alert(this.name);	// 将被解析为 person.name 的值
};
```

用**对象字面量**语法可以写成这样：

```js
var person = {
    name: "Nicholas",
    age: 29,
    sayName: function(){
    	alert(this.name);
	}
};
```



## 1.1 属性类型

ECMA-262 第 5 版在定义只有内部才用的特性（attribute）时，描述了属性（property）的各种特征。ECMA-262 定义这些特性是为了实现 JavaScript 引擎用的，因此在 JavaScript 中不能直接访问它们。为了表示特性是内部值，该规范把它们放在了两对方括号中。

ECMAScript 中有两种属性：数据属性和访问器属性。

### **数据属性**

数据属性包含一个数据值的位置。在这个位置可以读取和写入值。数据属性有 4 个描述其行为的特性。

- [[Configurable]]：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。
- [[Enumerable]]：表示能否通过 for-in 循环返回属性。
- [[Writable]]：表示能否修改属性的值。
- [[Value]]：包含这个属性的数据值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。默认值为 undefined。

直接在对象上定义的属性，[[Configurable]]、[[Enumerable]] 和 [[Writable]] 特性都被设置为 true，而 [[Value]] 特性被设置为指定的值。

```js
var person = {
    name: "Nicholas"	// [[Value]] 特性将被设置为 "Nicholas"
};
```

要修改属性默认的特性，必须使用 ECMAScript 5 的 Object.defineProperty() 方法。

### **访问器属性**

访问器属性不包含数据值，包含一对 getter 和 setter 函数（两个函数都非必需）。读取访问器属性时，会调用 getter 函数，函数负责返回有效的值；写入访问器属性时，会调用 setter 函数并传入新值，函数负责决定如何处理数据。访问器属性有如下 4 个特性。

- [[Configurable]]：与数据属性的 [[Configurable]] 相同。
- [[Enumerable]]：与数据属性的 [[Enumerable]] 相同。
- [[Get]]：在读取属性时调用的函数。默认值为 undefined。
- [[Set]]：在写入属性时调用的函数。默认值为 undefined。

访问器属性不能直接定义，必须使用 Object.defineProperty() 来定义。



### Object.defineProperty()

> *Object.defineProperty(obj, prop, descriptor)*

ES5 的 `Object.defineProperty()` 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。

方法接收三个参数：

- 属性所在的对象

- 属性的名字或 `Symbol` 。

  在 ES6 中，由于 Symbol 类型的特殊性，用 Symbo l类型的值来做对象的 key与常规的定义或修改不同，而 `Object.defineProperty` 是定义 key 为 Symbol 的属性的方法之一。

- 描述符对象。一个描述符只能是数据属性和访问器属性这两者其中之一；不能同时是两者。如果一个描述符同时拥有 `value` / `writable` 和 `get` / `set` 键，则会产生一个异常。

  - 拥有布尔值的键 `configurable`、`enumerable` 和 `writable` 的默认值都是 `false`。
  - 属性值和函数的键 `value`、`get` 和 `set` 字段的默认值为 `undefined`。

  这些选项不一定是自身属性，也要考虑继承来的属性。为了确认保留这些默认值，在设置之前，可能要冻结 [`Object.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)，明确指定所有的选项，或者通过 [`Object.create(null)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create) 将 [`__proto__`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/__proto__) 属性指向 [`null`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/null)。

**修改数据属性**

设置其中的一或多个值，可以修改对应的特性值。例如：

```js
var person = {};
Object.defineProperty(person, "name", {
    writable: false,	// 只读	
    value: "Nicholas"
});
alert(person.name); 	// "Nicholas"
person.name = "Greg";
alert(person.name);		// "Nicholas"
```

上例创建了一个 name 属性，值"Nicholas"是只读的，不可修改。如果尝试为它指定新值，在非严格模式下，赋值操作将被忽略；在严格模式下，会报错。

把 configurable 设置为 false，表示不能从对象中删除属性。如果对这个属性调用 delete，则在非严格模式下什么也不会发生，而在严格模式下会导致错误。而且，一旦把属性定义为不可配置的，就不能再把它变回可配置了。此时，再调用 Object.defineProperty() 方法修改除 writable 之外的特性，都会导致错误：

```js
var person = {};
Object.defineProperty(person, "name", {
	configurable: false,
	value: "Nicholas"
});
Object.defineProperty(person, "name", {
	configurable: true,	// 抛出错误
	value: "Nicholas"
});
```

**定义访问器属性**

```js
var book = {
    _year: 2004,
    edition: 1
};
Object.defineProperty(book, "year", {
    get: function(){
    	return this._year;
	},
    set: function(newValue){
        if (newValue > 2004) {
            this._year = newValue;
            this.edition += newValue - 2004;
        }
    }
});
book.year = 2005;
alert(book.edition); //2
```

不一定非要同时指定 getter 和 setter。只指定 getter 意味着属性是不能写，尝试写入属性会被忽略。在严格模式下，尝试写入只指定了 getter 函数的属性会抛出错误。类似地，只指定 setter 函数的属性也不能读，否则在非严格模式下会返回 undefined，而在严格模式下会抛出错误。

**浏览器支持情况**

支持 ECMAScript 5 的这个方法的浏览器有 IE9+（IE8 部分实现）、Firefox 4+、Safari 5+、Opera12+ 和 Chrome。在这个方法之前， 要创建访问器属性， 一般都使用两个非标准的方法：`__defineGetter__()` 和 `__defineSetter__()`。这两个方法最初由 Firefox 引入，后来 Safari 3、Chrome 1 和 Opera 9.5 也给出了相同的实现。

> IE8 第一个实现 Object.defineProperty() 方法。然而，这个版本的实现存在诸多限制：只能在 DOM 对象上使用这个方法，而且只能创建访问器属性。由于实现不彻底，建议不要在 IE8 中使用该方法。

在不支持 Object.defineProperty() 方法的浏览器中不能修改 [[Configurable]] 和 [[Enumerable]]。



## 1.2 定义多个属性

> *Object.defineProperties(obj, props)*

ECMAScript 5 定义了 Object.defineProperties() 方法。利用这个方法可以通过描述符一次定义多个属性。这个方法接收两个对象参数：第一个对象是要添加和修改其属性的对象，第二个对象的属性与第一个对象中要添加或修改的属性一一对应。

```js
var book = {};
Object.defineProperties(book, {	// 第一个参数是 book 对象
    _year: {			// 数据属性
    	value: 2004
	},
    edition: {			// 数据属性
    	value: 1
    },
    year: {				// 访问器属性
    	get: function(){
            return this._year;
		},
        set: function(newValue){
            if (newValue > 2004) {
                this._year = newValue;
                this.edition += newValue - 2004;
            }
        }
	}
});
```

支持 Object.defineProperties() 方法的浏览器有 IE9+、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome。



## 1.3 读取属性的特性

ECMAScript 5 的 Object.getOwnPropertyDescriptor() 方法可以取得给定属性的描述符。这个方法接收两个参数：属性所在的对象和要读取其描述符的属性名称，返回值是一个对象。

例如：对于上面的例子，可以用这样读取属性的特性

```js
var descriptor = Object.getOwnPropertyDescriptor(book, "_year");	// 读取 book 对象的 _year 数据属性。
alert(descriptor.value); 		// 2004
alert(descriptor.configurable); // false
alert(typeof descriptor.get); 	// "undefined"
var descriptor = Object.getOwnPropertyDescriptor(book, "year");		// 读取 book 对象的 year 访问器属性。
alert(descriptor.value);	 	// undefined
alert(descriptor.enumerable); 	// false
alert(typeof descriptor.get); 	// "function"
```

在 JavaScript 中，可以针对任何对象（包括 DOM 和 BOM 对象），使用Object.getOwnPropertyDescriptor() 方法。

支持这个方法的浏览器有 IE9+、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome。

