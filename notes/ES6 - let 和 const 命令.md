

#  let 和 const



## **ES6 声明变量的方法**

ES5 只有两种声明变量的方法：`var` 命令和 `function` 命令。

ES6 除了添加 `let` 和 `const` 命令，后面章节还会提到另外两种声明变量的方法： `import` 命令和 `class` 命令。所以，ES6 一共有 6 种声明变量的方法。



## 1. 声明变量 let

### **1.1 基本用法**



 `let` 命令用来声明变量，用法与 `var` 类似，但是变量只在 `let` 命令所在的代码块内有效。

**`let` 适合声明 `for` 循环的计数器**

`var` 命令声明的变量 `i` ，在全局范围内都有效。在下例中，所有数组成员里面的 `i` ，都指向同一个 `i`。

```js
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);   // 指向的是全局的i,运行时输出的是最后一轮的i的值
  };
}
a[6](); // 10
```

 `let` 命令声明的变量 `i` ，仅在块级作用域内有效，最后输出的是 6。

```js
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
console.log(i);	// ReferenceError: i is not defined
a[6](); 	// 6
```

for 循环中，设置循环变量的部分是一个父作用域，而循环体内部是一个单独的子作用域。

```js
for (let i = 0; i < 3; i++) {
    let i = 'abc';  // 函数内部的变量 i 与循环变量 i 不在同一个作用域
    console.log(i);
}
// abc
// abc
// abc
```



### **1.2 不存在变量提升**

`var` 命令会发生“变量提升”现象，即变量可以在声明之前使用，值为 `undefined`。 `let` 命令不存在变量提升，声明的变量一定要在声明后使用，否则报错。

```js
// var 的情况
console.log(foo); // 输出 undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```



### **1.3 暂时性死区**

只要块级作用域内存在 `let` 命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。在代码块内，**使用 `let` 命令声明变量之前，该变量都是不可用的**。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

```js
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```

“暂时性死区”，也意味着 `typeof` 不再是一个百分之百安全的操作。下例中，在声明之前，都属于 x 的“死区”，只要用到该变量就会报错。

```js
typeof undeclared_variable // "undefined"
typeof x; // ReferenceError
let x;
```

使用 `let` 声明变量时，只要变量在还没有声明完成前使用，就会报错。

```js
var x = x;  // 不报错
let x = x;  // 报错：ReferenceError: x is not defined
```



ES6 规定暂时性死区和 `let`、`const` 语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。



### **1.4 不允许重复声明**

`let` 不允许在相同作用域内，重复声明同一个变量。

```js
function func() {
  let a = 10;
  var a = 1;	// 报错，SyntaxError: Identifier 'a' has already been declared
}
function func() {
  let a = 10;
  let a = 1;	// 报错，SyntaxError: Identifier 'a' has already been declared
}
```

因此，不能在函数内部重新声明参数。

```js
function func(arg) {
  let arg;
}
func() // 报错

function func(arg) {
  {
    let arg;
  }
}
func() // 不报错
```



## 2. 块级作用域

块作用域由 { } 包括，if 语句和 for 语句里面的 { } 属于块作用域。

ES5 中作用域有：全局作用域、函数作用域。没有块作用域的概念。可以在函数内使用立即执行函数模拟块作用域。

ES6 中新增了块级作用域，let 和 const 有块级作用域。



**为什么需要块级作用域？** 

ES5 只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景。

不合理场景一：变量提升，内层变量可能会覆盖外层变量。

```js
var tmp = new Date();   // 外层变量 tmp

function f() {
  console.log(tmp);				// 变量提升，值为 undefined
  if (false) {
    var tmp = 'hello world';    // 内层局部变量 tmp
  }
}

f(); // undefined
```

不合理场景二：用来计数的循环变量泄露为全局变量。

```js
var s = 'hello';
for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}
console.log(i);     // 5
```



### **2.1 ES6 的块级作用域** 

`let` 实际上为 JavaScript 新增了块级作用域。

```js
function f1() {
  let n = 5;
  if (true) {
    let n = 10; // 外层代码块不受内层代码块的影响。
  }
  console.log(n); // 5
}
```

ES6 允许块级作用域的任意嵌套。每一层都是一个单独的作用域。

```js
{{{{
  {let insane = 'Hello World'}
  console.log(insane); // 报错
}}}};
```

内层作用域可以定义外层作用域的同名变量。

```js
{{{{
  let insane = 'Hello World';
  {let insane = 'Hello World'}
}}}};
```

块级作用域的出现，使得获得广泛应用的匿名立即执行函数表达式（匿名 IIFE）不再必要了。

```js
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```

### **2.2 块级作用域与函数声明**

函数能不能在块级作用域之中声明？ES5 规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。

下面两种函数声明，根据 ES5 的规定都是非法的。但是，浏览器没有遵守规定，为了兼容旧代码，还是支持在块级作用域之中声明函数，因此下面两种情况实际都能运行，不会报错。

```js
// 情况一
if (true) {
  function f() {}		// 在 ES5 中规定不能运行，但实际能运行
}

// 情况二
try {
  function f() {}
} catch(e) {
  // ...
}
```



ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于 `let`，在块级作用域之外不可引用。

```js
function f() { console.log('I am outside!'); }

(function () {
  if (false) {
    // 重复声明一次函数 f
    function f() { console.log('I am inside!'); }
  }
  f();
}());
// 在 ES6 浏览器中，报错 Uncaught TypeError: f is not a function
```

上面代码在 ES5 中运行，会得到 “I am inside!”，因为函数声明提升，在 `if` 内声明的函数 `f` 会被提升到函数头部。ES6 理论上会得到“I am outside!”。因为块级作用域内声明的函数类似于 `let`，对作用域之外没有影响。但是，在 ES6 浏览器中运行上面的代码，会报错。如果改变了块级作用域内声明的函数的处理规则，显然会对老代码产生很大影响。

为了减轻因此产生的不兼容问题，ES6 在[附录 B](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-block-level-function-declarations-web-legacy-compatibility-semantics)里面规定，浏览器的实现可以不遵守上面的规定，有自己的[行为方式](http://stackoverflow.com/questions/31419897/what-are-the-precise-semantics-of-block-level-functions-in-es6)。

- 允许在块级作用域内声明函数。
- 函数声明类似于 `var`，即会提升到全局作用域或函数作用域的头部。
- 同时，函数声明还会提升到所在的块级作用域的头部。

注意，上面三条规则只对 ES6 的浏览器实现有效，其他环境的实现不用遵守，还是将块级作用域的函数声明当作 `let` 处理。

根据这三条规则，浏览器的 ES6 环境中，块级作用域内声明的函数，行为类似于`var`声明的变量。上面的例子实际运行的代码如下。

```js
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }
(function () {
  var f = undefined;
  if (false) {
    function f() { console.log('I am inside!'); }
  }
  f();
}());
// Uncaught TypeError: f is not a function
```

考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。

```js
{
  let a = 'secret';
  function f() {			// 块级作用域内部的函数声明语句，建议不要使用
    return a;
  }
}
{
  let a = 'secret';
  let f = function () {		// 块级作用域内部，优先使用函数表达式
    return a;
  };
}
```

另外，ES6 的块级作用域必须有大括号。如果没有大括号，JavaScript 引擎就认为不存在块级作用域。

```js
// 第一种写法，报错
if (true) let x = 1;	// 没有大括号，不存在块级作用域，而let只能出现在当前作用域的顶层

// 第二种写法，不报错
if (true) {
  let x = 1;			// 有大括号，所以块级作用域成立。
}
```

函数声明也是如此，严格模式下，函数只能声明在当前作用域的顶层。

```js
// 不报错
'use strict';
if (true) {
  function f() {}
}
// 报错
'use strict';
if (true)
  function f() {}
```





## 3. 声明常量 const

其它 ES 版本中声明常量的方法

- ES3：变量名称全部大写，只是告诉开发者“这是一个常量”，但是实际上还是可以改变的。

  ```js
  var ES = "es6";			// 大写
  ES = "es2015";
  console.log(ES);		// es2015
  ```

- ES5：将 Object.defineProperty 的 writale 赋值为 false。

  ```js
  Object.defineProperty(window,'es',{
      value:'es6',
      writale: false
  });
  console.log(es);		// es6
  es = 'es2015';
  console.log(es);		// es6
  ```

在 ES 6 中用 const 声明常量。



### **3.1 基本用法**

`const` 声明一个只读的常量。一旦声明，常量的值就不能改变。这意味着，`const` 一旦声明变量，就必须立即初始化。

```js
const PI = 3.1415;
PI = 3; 	// TypeError: Assignment to constant variable.
const foo;	// SyntaxError: Missing initializer in const declaration
```

`const` 的作用域与 `let` 命令相同：只在声明所在的块级作用域内有效。

```js
if (true) {
    const MAX = 5;
}
MAX // Uncaught ReferenceError: MAX is not defined
```

`const` 命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。

```js
if (true) {
    console.log(MAX); // ReferenceError，只能在声明的位置后面使用
    const MAX = 5;
}
```

`const` 声明的常量，也与 `let` 一样不可重复声明。

```js
var message = "Hello!";
let age = 25;
// 不可重复声明，以下两行都会报错
const message = "Goodbye!";
const age = 30;
```

`const` 不属于顶层对象 window。

```js
var str1 = "es6"
const str2 = "es2015";
console.log(window.str1, window.str2);	// es6 undefined
```



### **3.2 本质**

`const` 实际上保证的并不是变量的值不得改动，而是**变量指向的那个内存地址所保存的数据**不得改动。

- 对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。
- 对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const` 只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，完全不能控制。

因此，将一个对象声明为常量必须非常小心。

下面代码中，常量 `foo` 储存的是一个地址，这个地址指向一个对象。不可变的只是这个地址，即不能把 `foo` 指向另一个地址，但对象本身是可变的，所以依然可以为其添加新属性。

```js
const foo = {};		
foo.prop = 123;		// 成功为 foo 添加一个属性
foo = {}; 	// 将 foo 指向另一个对象，TypeError: "foo" is read-only
```

const 变量为数组时，可以 push 元素，也可以设置 length 属性。

```js
const a = [];		// 常量`a`是一个数组，数组本身是可写的
a.push('Hello'); 	// 可执行
console.log(a);		// ["Hello"]
a.length = 0;    	// 可执行
console.log(a);		// []
a = ['Dave'];    	// 将另一个数组赋值给`a`，报错: TypeError
```

将对象冻结，应该使用 `Object.freeze` 方法。

```js
const foo = Object.freeze({});		// 常量`foo`指向一个冻结的对象
foo.prop = 123;			// 常规模式时，不起作用；严格模式时，会报错
```

 `Object.freeze` 方法是浅层次的冻结，只能冻结对象本身，不能冻结对象的属性。

```js
const esObj = {
	name : 'es6',
    year : 2015,
    extension : ['es7','es8','es9']
};
Object.freeze(esObj);
esObj.extension[0] = 'es2016';
console.log(esObj.extension);	// ["es2016", "es8", "es9"]
```

下面是一个将对象彻底冻结的函数。

```js
var constantize = (obj) => {
    Object.freeze(obj);		// 冻结第一层
    Object.keys(obj).forEach( (key, i) => {
        if ( typeof obj[key] === 'object' ) {
            constantize( obj[key] );		// 递归
        }
    });
};
```



## 4. 顶层对象的属性

顶层对象，在浏览器环境指的是 `window` 对象，在 Node 指的是 `global` 对象。

在 ES5 中，顶层对象的属性与全局变量是等价的。

```js
window.a = 1;			// 顶层对象
console.log(a); 		// 1
a = 2;					// 全局变量
console.log(window.a); 	// 2
```

顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一。这样的设计带来了几个很大的问题。

- 首先是没法在编译时就报出变量未声明的错误，只有运行时才能知道（因为全局变量可能是顶层对象的属性创造的，而属性的创造是动态的）；
- 其次，程序员很容易不知不觉地就创建了全局变量（比如打字出错）；
- 最后，顶层对象的属性是到处可以读写的，这非常不利于模块化编程。
- 另一方面，`window` 对象有实体含义，指的是浏览器的窗口对象，顶层对象是一个有实体含义的对象，也是不合适的。

ES6 为了改变这一点，一方面规定，为了保持兼容性，`var` 命令和 `function` 命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，`let ` 命令、`const ` 命令、`class` 命令声明的全局变量，不属于顶层对象的属性。也就是说，从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。

```js
var a = 1;
// 如果在 Node 的 REPL 环境，window.a 可以写成 global.a
// 或者采用通用方法，写成 this.a
console.log(window.a); 	// 1

let b = 1;
console.log(window.b); 	// undefined，不是顶层对象的属性
```



## 5. globalThis 对象

JavaScript 语言存在一个顶层对象，它提供全局环境（即全局作用域），所有代码都是在这个环境中运行。但是，顶层对象在各种实现里面是不统一的。

- 浏览器里面，顶层对象是 `window`，但 Node 和 Web Worker 没有 `window`。
- 浏览器和 Web Worker 里面，`self` 也指向顶层对象，但是 Node 没有`self`。
- Node 里面，顶层对象是 `global`，但其他环境都不支持。

同一段代码为了能够在各种环境，都能取到顶层对象，现在一般是使用 `this` 变量，但是有局限性。

- 全局环境中，`this` 会返回顶层对象。但是，Node 模块和 ES6 模块中，`this` 返回的是当前模块。
- 函数里面的 `this`，如果函数不是作为对象的方法运行，而是单纯作为函数运行，`this` 会指向顶层对象。但是，严格模式下，这时 `this` 会返回`undefined`。
- 不管是严格模式，还是普通模式，`new Function('return this')()`，总是会返回全局对象。但是，如果浏览器用了 CSP（Content Security Policy，内容安全策略），那么 `eval`、`new Function` 这些方法都可能无法使用。

综上所述，很难找到一种方法，可以在所有情况下，都取到顶层对象。

下面是两种勉强可以使用的方法。

```js
// 方法一
(typeof window !== 'undefined'
   ? window
   : (typeof process === 'object' &&
      typeof require === 'function' &&
      typeof global === 'object')
     ? global
     : this);

// 方法二
var getGlobal = function () {
  if (typeof self !== 'undefined') { return self; }
  if (typeof window !== 'undefined') { return window; }
  if (typeof global !== 'undefined') { return global; }
  throw new Error('unable to locate global object');
};
```

[ES2020](https://github.com/tc39/proposal-global) 在语言标准的层面，引入 `globalThis` 作为顶层对象。也就是说，任何环境下，`globalThis` 都是存在的，都可以从它拿到顶层对象，指向全局环境下的 `this`。

垫片库 [`global-this`](https://github.com/ungap/global-this) 模拟了这个提案，可以在所有环境拿到 `globalThis`。



