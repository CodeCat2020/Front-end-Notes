

# 关键字和保留字

ECMA-262 描述了一组具有特定用途的关键字，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。按照规则，关键字也是语言保留的，不能用作标识符。

| 关键字            | 描述                                              |
| :---------------- | :------------------------------------------------ |
| break             | 终止 switch 或循环。                              |
| catch             |                                                   |
| continue          | 跳出循环并在顶端开始。                            |
| debugger（ES 5）  | 停止执行 JavaScript，并调用调试函数（如果可用）。 |
| default           |                                                   |
| delete            |                                                   |
| do ... while      | 执行语句块，并在条件为真时重复代码块。            |
| finally           |                                                   |
| for               | 标记需被执行的语句块，只要条件为真。              |
| function          | 声明函数。                                        |
| if ... else       | 标记需被执行的语句块，根据某个条件。              |
| in                |                                                   |
| instanceof        |                                                   |
| new               |                                                   |
| return            | 退出函数。                                        |
| switch、case      | 标记需被执行的语句块，根据不同的情况。            |
| **super**（ES 6） | 用在类继承中。                                    |
| this              |                                                   |
| throw             |                                                   |
| try ... catch     | 对语句块实现错误处理。                            |
| typeof            |                                                   |
| var               | 声明变量。                                        |
| void              |                                                   |
| while             |                                                   |
| with              |                                                   |





ECMA-262 还描述了另外一组不能用作标识符的保留字。尽管保留字在这门语言中还没有任何特定的用途，但它们有可能在将来被用作关键字。以下是 ECMA-262 第 3 版定义的全部保留字：

**abstract**、boolean 、byte、char、class 、const、debugger、double、enum、export、extends、final、float、**goto**、**implements**、import、int、interface、 long、native、package、private、protected、public、short、 static、**super**、synchronized、throws、transient、volatile。	 

第 5 版把在非严格模式下运行时的保留字缩减为下列这些：

class 、const、enum、export、extends、import、super。

在严格模式下，第 5 版还对以下保留字施加了限制：

implements、interface、let、 package、private、protected、public、static、yield。



## new



> [new 运算符 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new)

**`new` 运算符**创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。

语法：

```
new constructor[([arguments])]
```

- `constructor`：一个指定对象实例的类型的类或函数。

- `arguments`：一个用于被 `constructor` 调用的参数列表。

创建一个用户自定义的对象需要两步：

1. 通过编写函数来定义对象类型。
2. 通过 `new` 来创建对象实例。

```js
function A() {};
var a = new A();
```



**`new`** 关键字会进行如下的操作：

- 创建一个空对象（即 `{}`）。
- 由 this 变量引用该对象。
- 该对象继承该函数的原型（更改原型链的指向）。
- 把属性和方法加入到 this 引用的对象中。
- 新创建的对象由 this 引用，最后隐式地返回 this ，过程如下。

```js
function demo(Base){
    var obj = {};					// 生成新对象
    // this = obj;
    obj.__proto__ = Base.prototype;	// 实例的__proto__指向原型，构造函数的 prototype 也指向原型（链接到原型）
    var res = Base.call(obj);	// 把函数的 this 绑定在了新生成的对象中
    if (typeof (res) == "object" || typeof (res) == "function") {
        return res;	  // 如果传入的函数(构造函数)有自己的返回值，则返回该值
    }
    return obj;	   // 如果传入的函数(构造函数)没有自己的返回值，则返回新对象
}
```





## in

> prop in object

如果指定的属性在指定的对象或其原型链中，则**`in` 运算符**返回`true`。

- `prop`：一个字符串类型或者 symbol 类型的属性名或者数组索引（非 symbol 类型将会强制转为字符串）。

- `objectName`：检查它（或其原型链）是否包含具有指定名称的属性的对象。`in` 右操作数必须是一个对象值。

```js
console.log(1 in [1]);// false
// 并不是表示数字 1 在不在数组里。而是表示数组中含不含有 1 这个索引 index 值。
```

返回情况：

- 如果使用 `delete` 运算符删除了一个属性，则 `in` 运算符对所删除属性返回 `false`。
- 如果将一个属性的值赋值为`undefined`，而没有删除它，则 `in` 运算仍然会返回`true`。
- 如果一个属性是从原型链上继承来的，`in` 运算符也会返回 `true`。

```js
// 对被删除的属性使用 in
var trees = new Array("redwood", "bay", "cedar");
delete trees[1];
console.log(1 in trees,trees[1]); 		// 返回 false undefined
// 对值为 undefined 的属性使用 in
trees[1] = undefined;
console.log(1 in trees,trees[1]); 		// 返回 true undefined
// 继承属性
console.log("toString" in {}); 			// 返回 true
```





## instanceof

instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链。内部机制是通过原型链实现的。





## typeof



typeof 是一个运算符，用于返回变量类型的字符串描述。



用 typeof 判断对象类型，可以准确地检测值类型（也叫原始类型或基本类型）数据，用 instanceOf 判断是不是数组。





在 JavaScript 中，typeof 用于判断一个变量的类型，instanceof 用于判断某个对象是否被另一个类构造（也就是说，是否是该类的实例化对象）。

typeof 运算符不能判断数组等引用类型。ECMAScript 引入 instanceof 来解决这个问题。与 typeof 运算符相似， instanceof 运算符用于识别正在处理的对象的类型。与 typeof 方法不同的是， instanceof 方法要求开发者明确地给出对象的特定类型。





## void



 void 操作符使表达式的运算结果返回 undefined。

- void(0) 用于防止页面刷新，并在调用时传递参数“0”。
- void(0) 用于调用另一种方法而不刷新页面。





## delete





## private



# 参考资料

[in - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in)

