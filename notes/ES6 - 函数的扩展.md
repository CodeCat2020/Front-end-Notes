# 函数的扩展

## 1. 函数参数的默认值

### 基本用法

ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法。

下面写法的缺点在于，如果参数 `y` 赋值了，但是对应的布尔值为 `false`，则该赋值不起作用。比如最后一行，参数 `y` 等于空字符，结果被改为默认值。

```javascript
function log(x, y) {
    y = y || 'World';		// 如果y没有赋值，指定默认值为World
    console.log(x, y);
}
log('Hello');				 // Hello World
log('Hello', 'China');		 // Hello China
log('Hello', '');			 // Hello World，默认值不起作用
```

为了避免这个问题，通常需要先判断参数 `y` 是否被赋值，如果没有，再等于默认值。

```javascript
if (typeof y === 'undefined') {
    y = 'World';
}
```

ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。

```javascript
function log(x, y = 'World') {		// 定义默认值。
    console.log(x, y);
}
log('Hello');			 // Hello World
log('Hello', 'China');	 // Hello China
log('Hello', '');		 // Hello
```

可以看到，ES6 的写法比 ES5 简洁许多，而且非常自然。下面是另一个例子。

```javascript
function Point(x = 0, y = 0) {
  this.x = x;
  this.y = y;
}
const p = new Point();
console.log(p); 			// Point { x: 0, y: 0 }
```

除了简洁，ES6 的写法还有两个好处：首先，阅读代码的人，可以立刻意识到哪些参数是可以省略的，不用查看函数体或文档；其次，有利于将来的代码优化，即使未来的版本在对外接口中，彻底拿掉这个参数，也不会导致以前的代码无法运行。

参数变量是默认声明的，所以不能用 `let` 或 `const` 再次声明。

```javascript
function foo(x = 5) {	
    // 参数变量 x 是默认声明的，在函数体中不能用 let 或 const 重复声明
    let x = 1;		// SyntaxError: 
    const x = 2;	// Identifier 'x' has already been declared
}
```

使用参数默认值时，函数不能有同名参数。

```javascript
// 不报错
function foo(x, x, y) {
    // ...
}

// 报错 
function foo(x, x, y = 1) {
    // ...
}
// SyntaxError: Duplicate parameter name not allowed in this context
```

另外，参数默认值不是传值的，而是每次都重新计算默认值表达式的值。也就是说，参数默认值是惰性求值的。

```javascript
let x = 99;
function foo(p = x + 1) {
    console.log(p);	// 每次调用函数`foo`，都会重新计算`x + 1`
}
foo()		 // 100

x = 100;
foo() 		// 101
```



### 与解构赋值默认值结合使用

参数默认值可以与解构赋值的默认值，结合起来使用。

下面代码只使用了对象的解构赋值默认值，没有使用函数参数的默认值。只有当函数 `foo` 的参数是一个对象时，变量 `x` 和 `y` 才会通过解构赋值生成。如果函数调用时没提供参数，变量 `x` 和 `y` 不会生成，会报错。

```javascript
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) 			// undefined 5
foo({x: 1}) 		// 1 5
foo({x: 1, y: 2}) 	// 1 2
foo() 		// TypeError: Cannot read property 'x' of undefined
```

通过提供函数参数的默认值，就可以避免这种情况。下面代码指定，如果没有提供参数，函数`foo`的参数默认为一个空对象。

```javascript
function foo({x, y = 5} = {}) {
  console.log(x, y);
}
foo() // undefined 5
```

下面是另一个解构赋值默认值的例子。

如果函数 `fetch` 的第二个参数是一个对象，可以为它的三个属性设置默认值。这种写法不能省略第二个参数。

```javascript
function fetch(url, { body = '', method = 'GET', headers = {} }) {
  console.log(method);
}
fetch('http://example.com', {});		// "GET"
fetch('http://example.com');			// 报错
```

如果结合函数参数的默认值，可以省略第二个参数。这时，就出现了双重默认值。下面代码中，函数没有第二个参数时，函数参数的默认值就会生效，然后才是解构赋值的默认值生效。

```javascript
function fetch(url, { body = '', method = 'GET', headers = {} } = {}) {
  console.log(method);
}
fetch('http://example.com');		// "GET"
```

下面两种写法的差别体现在：函数参数的默认值的不同，以及有无设置对象解构赋值的默认值。

```javascript
// 写法一
function m1({x = 0, y = 0} = {}) {	
    // 函数参数的默认值是空对象,设置了对象解构赋值的默认值
    return [x, y];
}

// 写法二
function m2({x, y} = { x: 0, y: 0 }) {
    // 函数参数的默认值是有具体属性的对象，但没有设置对象解构赋值的默认值
    return [x, y];
}
```

具体使用例子：

```javascript
// 函数没有参数的情况
m1() // [0, 0]
m2() // [0, 0]

// x 和 y 都有值的情况
m1({x: 3, y: 8}) // [3, 8]
m2({x: 3, y: 8}) // [3, 8]

// x 有值，y 无值的情况
m1({x: 3}) // [3, 0]
m2({x: 3}) // [3, undefined]

// x 和 y 都无值的情况
m1({}) // [0, 0];
m2({}) // [undefined, undefined]

m1({z: 3}) // [0, 0]
m2({z: 3}) // [undefined, undefined]
```



### 参数默认值的位置

通常情况下，定义了默认值的参数，应该是函数的尾参数。因为这样比较容易看出来，到底省略了哪些参数。

```js
function f(x, y = 1) {
    console.log([x, y]);
}
f(); 				// [undefined, 1]
f(2); 				// [2, 1]
f(1,); 				// [1, 1]
f(1,undefined); 	// [1, 1]
```

如果非尾部的参数设置默认值，实际上这个参数是没法省略的。

```javascript
function f(x = 1, y) {
    console.log([x, y]);
}
f(); 				// [1, undefined]
f(2); 				// [2, undefined]
f(, 1); 			// 报错，SyntaxError: Unexpected token ','
f(undefined, 1); 	// [1, 1]
```

如果传入 `undefined`，将触发该参数等于默认值，`null` 则没有这个效果。

```javascript
function foo(x = 5, y = 6) {
  console.log(x, y);
}
foo(undefined, null);		// 5 null
```



### 函数的 length 属性

指定了默认值后，函数的 `length` 属性将失真。`length` 属性返回没有指定默认值的参数个数，即函数的参数个数减去指定了默认值的参数个数。

```javascript
console.log(
	(function (a) {}).length, 			// 1
	(function (a = 5) {}).length ,		// 0
	(function (a, b, c = 5) {}).length 	// 2
);
```

这是因为 `length` 属性的含义是，该函数预期传入的参数个数。某个参数指定默认值以后，预期传入的参数个数就不包括这个参数了。同理，后文的 rest 参数也不会计入 `length` 属性。

```javascript
console.log((function(...args) {}).length); // 0
```

如果设置了默认值的参数不是尾参数，那么 `length` 属性不再计入后面的参数。

```javascript
console.log(
    (function (a = 0, b, c) {}).length, 	// 0
	(function (a, b = 1, c) {}).length, 	// 1
);
```



### 作用域

一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域（context）。等到初始化结束，这个作用域就会消失。这种语法行为，在不设置参数默认值时，是不会出现的。

下面代码中，参数 `y` 的默认值等于变量 `x`。调用函数 `f` 时，参数形成一个单独的作用域。在这个作用域里面，默认值变量 `x` 指向第一个参数 `x`，而不是全局变量`x`，所以输出是`2`。

```javascript
var x = 1;
function f(x, y = x) {
    console.log(y);
}
f(2); 		// 2
```

再看下面的例子。函数 `f` 调用时，参数 `y = x` 形成一个单独的作用域。这个作用域里面，变量 `x` 本身没有定义，所以指向外层的全局变量 `x`。函数调用时，函数体内部的局部变量 `x` 影响不到默认值变量 `x`。

此时，如果全局变量 `x` 不存在，就会报错 `ReferenceError: x is not defined`。

```javascript
let x = 1;				// 全局变量 x
function f(y = x) {		// 变量 x 本身没有定义，指向外层全局变量 x
    let x = 2;			// 函数内局部变量 x 不能影响参数默认值变量 x
    console.log(y);
}
f() // 1
```

下面这样写，也会报错。参数 `x = x` 形成一个单独作用域。实际执行的是 `let x = x`，由于暂时性死区的原因，这行代码会报错。

```javascript
var x = 1;
function foo(x = x) {
    // ...
}
foo() // ReferenceError: x is not defined
```

如果参数的默认值是一个函数，该函数的作用域也遵守这个规则。

请看下面的例子。函数 `bar` 的参数 `func` 的默认值是一个匿名函数，返回值为变量 `foo`。函数参数形成的单独作用域里面，并没有定义变量 `foo`，所以 `foo` 指向外层的全局变量 `foo`，因此输出 `outer`。

如果省略全局变量，会报错：`ReferenceError: foo is not defined`。

```javascript
let foo = 'outer';			// 全局变量 foo
function bar(func = () => foo) {
    let foo = 'inner';
    console.log(func());
}
bar(); 		// outer
```

下面是一个更复杂的例子。函数 `foo` 的参数形成一个单独作用域。这个作用域里面，首先声明了变量 `x` 和 `y`，`y` 的默认值是一个匿名函数。这个匿名函数内部的变量 `x`，指向同一个作用域的第一个参数 `x`。函数 `foo` 内部又声明了一个内部变量 `x`，该变量与第一个参数 `x` 由于不是同一个作用域，所以不是同一个变量，因此执行 `y` 后，内部变量 `x` 和外部全局变量 `x` 的值都没变。

```javascript
var x = 1;
function foo(x, y = function() { x = 2; }) {
    var x = 3;
    y();
    console.log(x);
}
foo()	 // 3
x		 // 1
```

如果将 `var x = 3` 的 `var` 去除，函数 `foo` 的内部变量 `x` 就指向第一个参数 `x`，与匿名函数内部的 `x` 是一致的，所以最后输出的就是`2`，而外层的全局变量 `x` 依然不受影响。

```javascript
var x = 1;
function foo(x, y = function() { x = 2; }) {
    x = 3;
    y();
    console.log(x);
}
foo() 	// 2
x 		// 1
```



### 应用

（1）利用参数默认值，可以指定某一个参数不得省略，如果省略就抛出一个错误。

下面代码的 `foo ` 函数，如果调用时没有参数，就调用默认值 `throwIfMissing` 函数，从而抛出一个错误。

```javascript
function throwIfMissing() {
    throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
    return mustBeProvided;
}

foo()
// Error: Missing parameter
```

从上面代码还可以看到，参数 `mustBeProvided` 的默认值等于 `throwIfMissing` 函数的运行结果（注意函数名 `throwIfMissing` 后有一对圆括号），这表明参数的默认值不是在定义时执行，而是在运行时执行。如果参数已经赋值，默认值中的函数就不会运行。

（2）另外，可以将参数默认值设为 `undefined`，表明这个参数是可以省略的。

```javascript
function foo(optional = undefined) { ··· }
```



## 2. rest 参数



ES6 引入 rest 参数（形式为 `...变量名`），用于获取函数的多余参数，这样就不需要使用 `arguments` 对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。

下面代码的 `add` 函数是一个求和函数，利用 rest 参数，可以向该函数传入任意数目的参数。

```javascript
function add(...values) {
    let sum = 0;
    for (var val of values) {
        sum += val;
    }
    console.log(sum);
}
add(2, 5, 3) 	// 10
```

下面是一个 rest 参数代替 `arguments` 变量的例子。比较后可以发现，rest 参数的写法更自然也更简洁。

`arguments` 对象不是数组，而是一个类似数组的对象。为了使用数组的方法，必须使用 `Array.prototype.slice.call` 先将其转为数组。rest 参数不存在这个问题，它是一个真正的数组，数组特有的方法都可以使用。

```javascript
// arguments变量的写法
function sortNumbers() {
    return Array.prototype.slice.call(arguments).sort();
}
// rest参数的写法
const sortNumbers = (...numbers) => numbers.sort();
```

下面是一个利用 rest 参数改写数组 `push` 方法的例子。

```javascript
function push(array, ...items) {
    items.forEach(function(item) {
        array.push(item);
        console.log(item);
    });
}

var a = [];
push(a, 1, 2, 3)
```

注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。

```javascript
// 报错
function f(a, ...b, c) {
    // ...
}
```

函数的 `length` 属性，不包括 rest 参数。

```javascript
console.log(
    (function(a) {}).length,  			// 1
	(function(...a) {}).length,  		// 0
	(function(a, ...b) {}).length,  	// 1
);
```



## 3. 严格模式

从 ES5 开始，函数内部可以设定为严格模式。ES2016 做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。

这样规定的原因是，函数内部的严格模式，同时适用于函数体和函数参数。但是，函数执行的时候，先执行函数参数，然后再执行函数体。这样就有一个不合理的地方，只有从函数体之中，才能知道参数是否应该以严格模式执行，但是参数却应该先于函数体执行。

```javascript
// 报错 SyntaxError: Illegal 'use strict' directive in function with non-simple parameter list
function doSomething(a, b = a) {
  'use strict';
  // code
}

// 报错
const doSomething = function ({a, b}) {
  'use strict';
  // code
};

// 报错
const doSomething = (...a) => {
  'use strict';
  // code
};

const obj = {
  // 报错
  doSomething({a, b}) {
    'use strict';
    // code
  }
};
```



```javascript
// 报错
function doSomething(value = 070) {
  'use strict';
  return value;
}
```

上面代码中，参数`value`的默认值是八进制数`070`，但是严格模式下不能用前缀`0`表示八进制，所以应该报错。但是实际上，JavaScript 引擎会先成功执行`value = 070`，然后进入函数体内部，发现需要用严格模式执行，这时才会报错。

虽然可以先解析函数体代码，再执行参数代码，但是这样无疑就增加了复杂性。因此，标准索性禁止了这种用法，只要参数使用了默认值、解构赋值、或者扩展运算符，就不能显式指定严格模式。

两种方法可以规避这种限制。第一种是设定全局性的严格模式，这是合法的。

```javascript
'use strict';

function doSomething(a, b = a) {
  // code
}
```

第二种是把函数包在一个无参数的立即执行函数里面。

```javascript
const doSomething = (function () {
  'use strict';
  return function(value = 42) {
    return value;
  };
}());
```

## 4. name 属性

函数的`name`属性，返回该函数的函数名。

```javascript
function foo() {}
foo.name // "foo"
```

这个属性早就被浏览器广泛支持，但是直到 ES6，才将其写入了标准。

需要注意的是，ES6 对这个属性的行为做出了一些修改。如果将一个匿名函数赋值给一个变量，ES5 的`name`属性，会返回空字符串，而 ES6 的`name`属性会返回实际的函数名。

```javascript
var f = function () {};

// ES5
f.name // ""

// ES6
f.name // "f"
```

上面代码中，变量`f`等于一个匿名函数，ES5 和 ES6 的`name`属性返回的值不一样。

如果将一个具名函数赋值给一个变量，则 ES5 和 ES6 的`name`属性都返回这个具名函数原本的名字。

```javascript
const bar = function baz() {};

// ES5
bar.name // "baz"

// ES6
bar.name // "baz"
```

`Function`构造函数返回的函数实例，`name`属性的值为`anonymous`。

```javascript
(new Function).name // "anonymous"
```

`bind`返回的函数，`name`属性值会加上`bound`前缀。

```javascript
function foo() {};
foo.bind({}).name // "bound foo"

(function(){}).bind({}).name // "bound "
```



## 6. 尾调用优化

### 什么是尾调用？

尾调用（Tail Call）是函数式编程的一个重要概念，本身非常简单，一句话就能说清楚，就是指某个函数的最后一步是调用另一个函数。

```javascript
function f(x){
  return g(x);
}
```

上面代码中，函数`f`的最后一步是调用函数`g`，这就叫尾调用。

以下三种情况，都不属于尾调用。

```javascript
// 情况一
function f(x){
  let y = g(x);
  return y;
}

// 情况二
function f(x){
  return g(x) + 1;
}

// 情况三
function f(x){
  g(x);
}
```

上面代码中，情况一是调用函数`g`之后，还有赋值操作，所以不属于尾调用，即使语义完全一样。情况二也属于调用后还有操作，即使写在一行内。情况三等同于下面的代码。

```javascript
function f(x){
  g(x);
  return undefined;
}
```

尾调用不一定出现在函数尾部，只要是最后一步操作即可。

```javascript
function f(x) {
  if (x > 0) {
    return m(x)
  }
  return n(x);
}
```

上面代码中，函数`m`和`n`都属于尾调用，因为它们都是函数`f`的最后一步操作。

### 尾调用优化

尾调用之所以与其他调用不同，就在于它的特殊的调用位置。

我们知道，函数调用会在内存形成一个“调用记录”，又称“调用帧”（call frame），保存调用位置和内部变量等信息。如果在函数`A`的内部调用函数`B`，那么在`A`的调用帧上方，还会形成一个`B`的调用帧。等到`B`运行结束，将结果返回到`A`，`B`的调用帧才会消失。如果函数`B`内部还调用函数`C`，那就还有一个`C`的调用帧，以此类推。所有的调用帧，就形成一个“调用栈”（call stack）。

尾调用由于是函数的最后一步操作，所以不需要保留外层函数的调用帧，因为调用位置、内部变量等信息都不会再用到了，只要直接用内层函数的调用帧，取代外层函数的调用帧就可以了。

```javascript
function f() {
  let m = 1;
  let n = 2;
  return g(m + n);
}
f();

// 等同于
function f() {
  return g(3);
}
f();

// 等同于
g(3);
```

上面代码中，如果函数`g`不是尾调用，函数`f`就需要保存内部变量`m`和`n`的值、`g`的调用位置等信息。但由于调用`g`之后，函数`f`就结束了，所以执行到最后一步，完全可以删除`f(x)`的调用帧，只保留`g(3)`的调用帧。

这就叫做“尾调用优化”（Tail call optimization），即只保留内层函数的调用帧。如果所有函数都是尾调用，那么完全可以做到每次执行时，调用帧只有一项，这将大大节省内存。这就是“尾调用优化”的意义。

注意，只有不再用到外层函数的内部变量，内层函数的调用帧才会取代外层函数的调用帧，否则就无法进行“尾调用优化”。

```javascript
function addOne(a){
  var one = 1;
  function inner(b){
    return b + one;
  }
  return inner(a);
}
```

上面的函数不会进行尾调用优化，因为内层函数`inner`用到了外层函数`addOne`的内部变量`one`。

注意，目前只有 Safari 浏览器支持尾调用优化，Chrome 和 Firefox 都不支持。

### 尾递归

函数调用自身，称为递归。如果尾调用自身，就称为尾递归。

递归非常耗费内存，因为需要同时保存成千上百个调用帧，很容易发生“栈溢出”错误（stack overflow）。但对于尾递归来说，由于只存在一个调用帧，所以永远不会发生“栈溢出”错误。

```javascript
function factorial(n) {
  if (n === 1) return 1;
  return n * factorial(n - 1);
}

factorial(5) // 120
```

上面代码是一个阶乘函数，计算`n`的阶乘，最多需要保存`n`个调用记录，复杂度 O(n) 。

如果改写成尾递归，只保留一个调用记录，复杂度 O(1) 。

```javascript
function factorial(n, total) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

factorial(5, 1) // 120
```

还有一个比较著名的例子，就是计算 Fibonacci 数列，也能充分说明尾递归优化的重要性。

非尾递归的 Fibonacci 数列实现如下。

```javascript
function Fibonacci (n) {
  if ( n <= 1 ) {return 1};

  return Fibonacci(n - 1) + Fibonacci(n - 2);
}

Fibonacci(10) // 89
Fibonacci(100) // 超时
Fibonacci(500) // 超时
```

尾递归优化过的 Fibonacci 数列实现如下。

```javascript
function Fibonacci2 (n , ac1 = 1 , ac2 = 1) {
  if( n <= 1 ) {return ac2};

  return Fibonacci2 (n - 1, ac2, ac1 + ac2);
}

Fibonacci2(100) // 573147844013817200000
Fibonacci2(1000) // 7.0330367711422765e+208
Fibonacci2(10000) // Infinity
```

由此可见，“尾调用优化”对递归操作意义重大，所以一些函数式编程语言将其写入了语言规格。ES6 亦是如此，第一次明确规定，所有 ECMAScript 的实现，都必须部署“尾调用优化”。这就是说，ES6 中只要使用尾递归，就不会发生栈溢出（或者层层递归造成的超时），相对节省内存。

### 递归函数的改写

尾递归的实现，往往需要改写递归函数，确保最后一步只调用自身。做到这一点的方法，就是把所有用到的内部变量改写成函数的参数。比如上面的例子，阶乘函数 factorial 需要用到一个中间变量`total`，那就把这个中间变量改写成函数的参数。这样做的缺点就是不太直观，第一眼很难看出来，为什么计算`5`的阶乘，需要传入两个参数`5`和`1`？

两个方法可以解决这个问题。方法一是在尾递归函数之外，再提供一个正常形式的函数。

```javascript
function tailFactorial(n, total) {
  if (n === 1) return total;
  return tailFactorial(n - 1, n * total);
}

function factorial(n) {
  return tailFactorial(n, 1);
}

factorial(5) // 120
```

上面代码通过一个正常形式的阶乘函数`factorial`，调用尾递归函数`tailFactorial`，看起来就正常多了。

函数式编程有一个概念，叫做柯里化（currying），意思是将多参数的函数转换成单参数的形式。这里也可以使用柯里化。

```javascript
function currying(fn, n) {
  return function (m) {
    return fn.call(this, m, n);
  };
}

function tailFactorial(n, total) {
  if (n === 1) return total;
  return tailFactorial(n - 1, n * total);
}

const factorial = currying(tailFactorial, 1);

factorial(5) // 120
```

上面代码通过柯里化，将尾递归函数`tailFactorial`变为只接受一个参数的`factorial`。

第二种方法就简单多了，就是采用 ES6 的函数默认值。

```javascript
function factorial(n, total = 1) {
  if (n === 1) return total;
  return factorial(n - 1, n * total);
}

factorial(5) // 120
```

上面代码中，参数`total`有默认值`1`，所以调用时不用提供这个值。

总结一下，递归本质上是一种循环操作。纯粹的函数式编程语言没有循环操作命令，所有的循环都用递归实现，这就是为什么尾递归对这些语言极其重要。对于其他支持“尾调用优化”的语言（比如 Lua，ES6），只需要知道循环可以用递归代替，而一旦使用递归，就最好使用尾递归。

### 严格模式

ES6 的尾调用优化只在严格模式下开启，正常模式是无效的。

这是因为在正常模式下，函数内部有两个变量，可以跟踪函数的调用栈。

- `func.arguments`：返回调用时函数的参数。
- `func.caller`：返回调用当前函数的那个函数。

尾调用优化发生时，函数的调用栈会改写，因此上面两个变量就会失真。严格模式禁用这两个变量，所以尾调用模式仅在严格模式下生效。

```javascript
function restricted() {
  'use strict';
  restricted.caller;    // 报错
  restricted.arguments; // 报错
}
restricted();
```

### 尾递归优化的实现

尾递归优化只在严格模式下生效，那么正常模式下，或者那些不支持该功能的环境中，有没有办法也使用尾递归优化呢？回答是可以的，就是自己实现尾递归优化。

它的原理非常简单。尾递归之所以需要优化，原因是调用栈太多，造成溢出，那么只要减少调用栈，就不会溢出。怎么做可以减少调用栈呢？就是采用“循环”换掉“递归”。

下面是一个正常的递归函数。

```javascript
function sum(x, y) {
  if (y > 0) {
    return sum(x + 1, y - 1);
  } else {
    return x;
  }
}

sum(1, 100000)
// Uncaught RangeError: Maximum call stack size exceeded(…)
```

上面代码中，`sum`是一个递归函数，参数`x`是需要累加的值，参数`y`控制递归次数。一旦指定`sum`递归 100000 次，就会报错，提示超出调用栈的最大次数。

蹦床函数（trampoline）可以将递归执行转为循环执行。

```javascript
function trampoline(f) {
  while (f && f instanceof Function) {
    f = f();
  }
  return f;
}
```

上面就是蹦床函数的一个实现，它接受一个函数`f`作为参数。只要`f`执行后返回一个函数，就继续执行。注意，这里是返回一个函数，然后执行该函数，而不是函数里面调用函数，这样就避免了递归执行，从而就消除了调用栈过大的问题。

然后，要做的就是将原来的递归函数，改写为每一步返回另一个函数。

```javascript
function sum(x, y) {
  if (y > 0) {
    return sum.bind(null, x + 1, y - 1);
  } else {
    return x;
  }
}
```

上面代码中，`sum`函数的每次执行，都会返回自身的另一个版本。

现在，使用蹦床函数执行`sum`，就不会发生调用栈溢出。

```javascript
trampoline(sum(1, 100000))
// 100001
```

蹦床函数并不是真正的尾递归优化，下面的实现才是。

```javascript
function tco(f) {
  var value;
  var active = false;
  var accumulated = [];

  return function accumulator() {
    accumulated.push(arguments);
    if (!active) {
      active = true;
      while (accumulated.length) {
        value = f.apply(this, accumulated.shift());
      }
      active = false;
      return value;
    }
  };
}

var sum = tco(function(x, y) {
  if (y > 0) {
    return sum(x + 1, y - 1)
  }
  else {
    return x
  }
});

sum(1, 100000)
// 100001
```

上面代码中，`tco`函数是尾递归优化的实现，它的奥妙就在于状态变量`active`。默认情况下，这个变量是不激活的。一旦进入尾递归优化的过程，这个变量就激活了。然后，每一轮递归`sum`返回的都是`undefined`，所以就避免了递归执行；而`accumulated`数组存放每一轮`sum`执行的参数，总是有值的，这就保证了`accumulator`函数内部的`while`循环总是会执行。这样就很巧妙地将“递归”改成了“循环”，而后一轮的参数会取代前一轮的参数，保证了调用栈只有一层。

## 7. 函数参数的尾逗号

ES2017 [允许](https://github.com/jeffmo/es-trailing-function-commas)函数的最后一个参数有尾逗号（trailing comma）。

此前，函数定义和调用时，都不允许最后一个参数后面出现逗号。

```javascript
function clownsEverywhere(
  param1,
  param2
) { /* ... */ }

clownsEverywhere(
  'foo',
  'bar'
);
```

上面代码中，如果在`param2`或`bar`后面加一个逗号，就会报错。

如果像上面这样，将参数写成多行（即每个参数占据一行），以后修改代码的时候，想为函数`clownsEverywhere`添加第三个参数，或者调整参数的次序，就势必要在原来最后一个参数后面添加一个逗号。这对于版本管理系统来说，就会显示添加逗号的那一行也发生了变动。这看上去有点冗余，因此新的语法允许定义和调用时，尾部直接有一个逗号。

```javascript
function clownsEverywhere(
  param1,
  param2,
) { /* ... */ }

clownsEverywhere(
  'foo',
  'bar',
);
```

这样的规定也使得，函数参数与数组和对象的尾逗号规则，保持一致了。

## 8. Function.prototype.toString()

[ES2019](https://github.com/tc39/Function-prototype-toString-revision) 对函数实例的`toString()`方法做出了修改。

`toString()`方法返回函数代码本身，以前会省略注释和空格。

```javascript
function /* foo comment */ foo () {}

foo.toString()
// function foo() {}
```

上面代码中，函数`foo`的原始代码包含注释，函数名`foo`和圆括号之间有空格，但是`toString()`方法都把它们省略了。

修改后的`toString()`方法，明确要求返回一模一样的原始代码。

```javascript
function /* foo comment */ foo () {}

foo.toString()
// "function /* foo comment */ foo () {}"
```

## 9. catch 命令的参数省略

JavaScript 语言的`try...catch`结构，以前明确要求`catch`命令后面必须跟参数，接受`try`代码块抛出的错误对象。

```javascript
try {
  // ...
} catch (err) {
  // 处理错误
}
```

上面代码中，`catch`命令后面带有参数`err`。

很多时候，`catch`代码块可能用不到这个参数。但是，为了保证语法正确，还是必须写。[ES2019](https://github.com/tc39/proposal-optional-catch-binding) 做出了改变，允许`catch`语句省略参数。

```javascript
try {
  // ...
} catch {
  // ...
}
```



