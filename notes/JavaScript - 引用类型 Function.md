# 函数



**函数是对象，函数名是指针**

函数实际上是 `Function` 类型的实例，因此函数也是对象，和其它对象一样具有属性和方法。由于函数是对象，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。

函数名仅仅是指向函数的指针。一个函数可能会有多个名字。

```js
function sum(num1, num2){
	return num1 + num2;
}
console.log(sum(10,10)); 		  	// 20
var anotherSum = sum;
console.log(anotherSum(10,10)); 	// 20
sum = null;
console.log(anotherSum(10,10)); 	// 20
```

函数是 JavaScript 中的一等对象，这意味着可以将函数作为变量传递给其他函数，也可以从其他函数返回函数。 一个常见的用法是把*匿名函数*作为回调函数传递到异步函数中。函数与其他对象的区别在于，函数可以被调用。







**函数的返回值**

函数在定义时无须指定函数的返回值类型，任何函数在任何时候都可以通过 return 语句后跟要返回的值来实现返回值。

位于 return 语句之后的任何代码永远不会执行。

一个函数中可以包含多个 return 语句。推荐的做法是要么让函数始终都返回一个值，要么永远都不要返回值。否则，如果函数有时候返回值，有时候不返回值，会给调试代码带来不便。

return 语句可以不带有任何返回值。在这种情况下，函数在停止执行后将返回 undefined 值。

```js
// 不需要指定函数的返回值
function diff(num1, num2) {		// 对比 Java： private int diff(num1, num2)
    if (num1 < num2) {
    	return num2 - num1;
        console.log("Hi~"); 	// 永远不会执行
    } else if (num1 > num2){
    	return;
    }else{
    	console.log("Hello~");	// 不推荐（return 时有时无）
    }
}
```

**使用注意事项**

严格模式对函数有一些限制：

- 不能把函数和参数命名为 eval 或 arguments；
- 不能出现两个命名参数同名的情况。

如果发生以上情况，就会导致语法错误，代码无法执行。





## 1. 定义函数

定义函数的方式有两种：一种是函数声明，另一种就是函数表达式。

- 函数声明：使用 function 关键字来声明，后跟一组参数以及函数体。（以 function 开头）

  ```js
  function name(argument1,argument2){	statements}		// 没有分号
  ```

  例子：

  ```js
  function sum (num1, num2) {
      return num1 + num2;
  }
  ```

- 函数表达式：可以无须对函数命名，从而实现动态编程。（不以 function 开头，function 前面可以是

  ```js
  var sum = function(num1, num2){
      return num1 + num2;
  };
  ```

-  Function 构造函数：可以接收任意数量的参数，但最后一个参数始终都被看成是函数体，而前面的参数枚举新函数的参数。

  ```js
  var sum = new Function("num1", "num2", "return num1 + num2"); // 不推荐
  ```

  实际上也是函数表达式。不推荐使用。这种语法会导致解析两次代码，从而影响性能（第一次是解析常规 ECMAScript 代码，第二次是解析传入构造函数中的字符串）。





**函数声明 vs 函数表达式**

- 函数声明要求有名字，但函数表达式可以无须对函数命名，从而实现动态编程。

- 函数表达式后面可以加括号立即调用该函数，函数声明不可以，只能以函数名形式调用。

  ```js
  var fnName = function(){
      console.log('Hello World');
  }();
  // Hello World
  // 函数表达式后面加括号，当 Javascript 引擎解析到此处时能立即调用函数
  function fnName(){
      console.log('Hello World');
  }();
  // SyntaxError: Unexpected token ')'
  // Javascript 引擎将开头的 function 关键字当做函数声明，后面的 () 不能出现在函数声明。
  function(){
      console.log('Hello World');  
  }();
  // SyntaxError: Function statements require a function name
  // Javascript 引擎将开头的 function 关键字当做函数声明，function 后面需要函数名。
  ```

- 函数声明有函数提升（function declaration hoisting），函数表达式没有。

  - 在执行代码前，解析器会率先读取函数声明并将它们放到源代码树的顶部，并使其在执行任何代码之前可用（可以访问），可以把函数声明放在调用语句后面；

  - 函数表达式必须等到解析器执行到它所在的代码行，才会真正被解释执行。函数表达式与其他表达式一样，在使用前必须先赋值。

    声明语句在代码运行之前解析，赋值语句只在运行时执行。

  ```js
  console.log(sum1(10,10));	// 20，因为 sum1 在代码运行前已经被创建
  function sum1(num1, num2){
      return num1 + num2;
  }
  console.log(sum2);			// undefined
  console.log(sum2(10,10));	// 报错 Uncaught TypeError: sum2 is not a function
  var sum2 = function(num1, num2){
      return num1 + num2;
  };
  ```

- 函数声明可以转为函数表达式。

  ```js
  function foo() {}			// 函数声明
  (function bar() {})			// 函数表达式
  x = function hello() {}		// 函数表达式
  function a() {				// 函数声明
      function b() {}			// 函数声明
      if (0) {
          function c() {}		// 函数表达式。注意！（？）
      }
  }
  ```









## 2. 调用函数

函数定义后不能自动执行（除了 IIFE），需要调用它。直接在需要的位置写函数名即可。

**调用位置**

第一种情况：在 `<script>` 标签内调用。

第二种情况：在 HTML 文件中调用，如通过点击按钮后调用定义好的函数。

```html
<input type="button" value="click it" onclick="add2()"> 
```

要访问函数的指针而不执行函数的话，必须去掉函数名后面的那对圆括号。



函数的调用方式：

- 直接调用

  ```js
  function func(){}
  func();
  ```

- 作为对象方法调用

  当一个函数是一个对象的属性时，称之为**方法**。

  ```js
  var a = {
  	func:function(){}
  }
  a.func();
  ```

- 作为构造函数调用。在 new 的过程中，使用 call 改变了 this 的指向。

  ```js
  function Func(){}
  var a = new Func();
  ```

- 作为函数方法调用函数，通过 call 和 apply 方法调用

  ```js
  function func() {
      var name = 'Cherry';
      innerFunction();				// 直接调用
      function innerFunction() {
          console.log(this.name);      // windowsName
      }
  }
  func();
  ```

- 调用自身（递归）



## 3. 函数作用域

在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义。相对应的，一个函数可以访问定义在其范围内的任何变量和函数。换言之，定义在全局域中的函数可以访问所有定义在全局域中的变量。在另一个函数中定义的函数也可以访问在其父函数中定义的所有变量和父函数有权访问的任何其他变量。





JS里的 function 能访问它们的：

- 参数
- 局部变量或函数
- 全局变量
- 外部函数的变量或函数，比如内层的函数可以访问嵌套关系外层的函数。





### 作为值的函数

因为 ECMAScript 中的函数名本身就是变量，所以函数也可以作为值来使用。

不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。

**把一个函数传递给另一个函数**

这个函数接受两个参数。第一个参数是函数，第二个参数是要传递给该函数的一个值。

```js
function callSomeFunction(someFunction, someArgument){
	return someFunction(someArgument);
}
```

下面例子中传递给 callSomeFunction() 的是 add10 和 getGreeting，而不是执行它们之后的结果。

```js
function add10(num){
    return num + 10;
}
var result1 = callSomeFunction(add10, 10);
alert(result1); 				// 20。实际上执行 add10(10)
function getGreeting(name){
    return "Hello, " + name;
}
var result2 = callSomeFunction(getGreeting, "Nicholas");
alert(result2);					// "Hello, Nicholas"
```



**从一个函数中返回另一个函数**

假设有一个对象数组，想要根据某个对象属性对数组进行排序。

```js
function createComparisonFunction(propertyName) {
    return function(object1, object2){
        var value1 = object1[propertyName];
        var value2 = object2[propertyName];
        if (value1 < value2){
            return -1;
        } else if (value1 > value2){
            return 1;
        } else {
            return 0;
        }
    };
}
```

使用上面的函数：

```js
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
data.sort(createComparisonFunction("name"));
alert(data[0].name); 		 // Nicholas
data.sort(createComparisonFunction("age"));
alert(data[0].name);		 // Zachary
```





## 没有重载

在其他语言（如 Java）中，可以为一个函数编写两个定义，只要这两个定义的签名（接受的参数的类型和数量）不同即可。

ECMAScirpt 函数没有签名，因为其参数是由包含零或多个值的数组来表示的。由于不存在函数签名的特性，**ECMAScript 函数不能重载**。

如果在 ECMAScript 中定义了两个名字相同的函数，则该名字只属于后定义的函数。

```js
function addSomeNumber(num){
	return num + 100;
}
function addSomeNumber(num) {
	return num + 200;
}
var result = addSomeNumber(100); //300
```

将函数名想象为指针，有助于理解为什么 ECMAScript 中没有函数重载的概念。

```js
var addSomeNumber = function (num){
    return num + 100;
};
addSomeNumber = function (num) {
    return num + 200;
};
var result = addSomeNumber(100); //300
```

如前所述，通过检查传入函数中参数的类型和数量并作出不同的反应，可以模仿方法的重载。









## 函数内部属性

在函数内部，有两个特殊的对象：arguments 和 this。

### arguments



ES 中的参数在内部是用一个数组来表示的。函数接收到的始终都是这个数组，不关心数组中包含哪些参数（参数个数和参数类型）。

arguments 是一个类数组对象，包含着传入函数中的所有参数。

在函数体内可以通过 arguments 对象来访问参数数组，获取传递给函数的每一个参数。arguments 对象与数组类似，可以使用方括号访问每一个元素。





arguments 虽然有数组的性质，但不是真正的数组。它只是一个类数组对象，并没有数组的方法，不能像真正的数组那样调用 join()、concat () 、pop() 等方法。

- 数组是一种引用类型。arguments 是所有函数（非箭头函数）中都可用的**局部变量**，只能在函数中使用。



**arguments 对象的属性**

- `arguments.length`：传递给函数的参数数量。

  ```js
  function howManyArgs() {
  	alert(arguments.length);
  }
  howManyArgs("string", 45); 	// 2。有两个参数。
  howManyArgs(); 				// 0。没有参数。
  howManyArgs(12); 			// 1。有一个参数。
  ```

- `arguments.callee`：指向参数所属的当前执行的函数。指向调用当前函数的函数。
- arguments[@@iterator]：返回一个新的[Array 迭代器](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/@@iterator) 对象，该对象包含参数中每个索引的值。



#### **理解参数**

命名的参数只提供便利，但不是必需的，所以可以不显式地使用命名参数。利用“不显式使用命名参数”特点，可以让函数接收任意个参数并分别实现适当的功能（模拟函数重载）。

```js
function doAdd() {
    if(arguments.length == 1) {
    	alert(arguments[0] + 10);
    } else if (arguments.length == 2) {
    	alert(arguments[0] + arguments[1]);
    }
}
doAdd(10); 		// 20
doAdd(30, 20); 	// 50
```

arguments 对象可以与命名参数一起使用。

arguments 的值与对应命名参数的值的内存空间是独立的，但是它们的值会同步。另外，arguments 对象的长度是由传入的参数个数决定的，不是由定义函数时的命名参数的个数决定的。

没有传递值的命名参数将自动被赋予 undefined 值。

```js
function doAdd(num1, num2) {
	arguments[1] = 10;			// 与 num2 对应
	console.log(arguments.length, num1, num2, arguments[0] + num2);
}
doAdd();	// 0 undefined undefined NaN
doAdd(1);	// 1 1 undefined NaN。只传入一个参数，为 arguments[1] 设置的值不会反应到命名参数中
doAdd(1,1);	// 2 1 10 11
```

严格模式对 arguments 对象的使用做出了一些限制。

- 首先，不能通过 arguments 设置参数的值。
- 其次，重写 arguments 的值会导致语法错误（代码将不会执行）。

注意：ECMAScript 中的所有参数传递的都是值，不可能通过引用传递参数。

```js
function doAdd(num1, num2) {
	'use strict'
	arguments[1] = 10;				// 无效
	console.log(arguments.length, num1, num2, arguments[0] + num2);
}
doAdd();	// 0 undefined undefined NaN
doAdd(1);	// 1 1 undefined NaN
doAdd(1,1);	// 2 1 1 2
```





#### callee

**`callee`** 是 `arguments` 对象的一个属性，该属性是一个指针，指向拥有这个 arguments 对象的函数。这在函数的名称是未知时很有用，例如匿名函数。

定义阶乘函数一般都要用到递归算法。如果递归时使用函数名，在函数名不变的情况下，没有问题。但问题是这个函数的执行与函数名紧紧耦合在了一起。为了消除这种紧密耦合的现象，可以使用 arguments.callee。

```js
function factorial(num){
    if (num <= 1) {
        return 1;
    } else {
        //return num * factorial(num - 1);	// 函数名不能改变
        return num * arguments.callee(num-1);
    }
}
```

重写后的 factorial() 函数的函数体内，没有再引用函数名 factorial。这样，无论引用函数时使用的是什么名字，都可以保证正常完成递归调用。例如：

```js
var trueFactorial = factorial;
factorial = function(){
    return 0;
};
alert(trueFactorial(5)); //120
```

### this

this 是 JavaScript 的一个关键字，是函数运行时自动生成的一个内部对象，只能在函数内部使用。

this 表示当前对象的一个引用，引用的是函数据以执行的环境对象。在调用函数之前，this 的值并不确定，因此 this 可能会在代码执行过程中引用不同的对象。



**总原则**：在不改变 this 指向的前提下，this 总是指向函数的直接调用者（而非间接调用者）。this 永远指向最后调用它的那个对象。





this 的指向大致可以分为五种：

箭头函数 -> new绑定 -> 显示绑定call/bind/apply -> 隐式绑定 -> 默认绑定

- 默认绑定：一般发生在回调函数，函数直接调用。

  在全局范围内调用函数时，this 指向全局对象（浏览器下指 window）。

  ```js
  function test() {
      console.log(this);	// 严格模式下是 undefined；非严格模式下是 window
  }
  setTimeout(function () {
      console.log(this);	// 严格模式和非严格模式下都是 window
  });
  arr.forEach(function () {
      console.log(this);	// 严格模式下是 undefined；非严格模式下是 window
  });
  ```

  在严格模式下，未指定环境对象而调用函数，则 this 值不会转型为 window。除非明确把函数添加到某个对象或者调用 apply() 或 call()，否则 this 值将是 undefined。

  ```js
  function Foo2(){
      'use strict'       		
      console.log(this.location);	// TypeError: Cannot read property 'location' of undefined    
  }
  Foo2();
  ```

  在事件中，this 指向触发这个事件的对象， 特殊的是，IE 中 attachEvent 中的 this 总是指向全局对象 window。

- 隐式绑定：谁调用就指向谁。

  对象调用函数时，this 指向当前对象。下例，当把函数赋给对象 o 并调用 o.sayColor() 时，this 引用的是对象 o。

  ```js
  window.color = "red";
  var o = { color: "blue" };
  function sayColor(){	// 函数 sayColor() 是在全局作用域中定义的
      alert(this.color);	// 在调用函数之前，this 的值并不确定
  }
  sayColor(); 		// "red"，this 引用 window
  o.sayColor = sayColor;
  o.sayColor(); 		// "blue"，this 引用 o
  ```

- 显示绑定：apply、call、bind。当用 apply 和 call 上下文调用时，指向传入的第一个参数。

- new 绑定：使用 new 实例化对象时，this 指向新创建的对象。

- ES6 箭头函数。





怎么改变 this 指向性？

- 使用 ES6 的箭头函数

  **箭头函数的 this 始终指向函数定义时的 this，而非执行时。**箭头函数中没有 this 绑定，必须通过查找作用域链来决定其值，如果箭头函数被非箭头函数包含，则 this 绑定的是最近一层非箭头函数的 this，否则，this 为 undefined（？window）。

- 在函数内部使用 `_this = this`

  先将调用这个函数的对象保存在变量 `_this` 中，然后在函数中都使用这个 `_this`

- 使用 `apply`、`call`、`bind`

- new 实例化一个对象





### caller

ECMAScript 5 也规范化了另一个函数对象的属性：caller。除了Opera 的早期版本不支持，IE、Firefox、Chrome 和 Safari 的所有版本以及 Opera 9.6 都支持 caller 属性。

这个属性中保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值为 null。

下例中，因为 outer() 调用了 inter()，所以 inner.caller 就指向 outer()。为了实现更松散的耦合，也可以通过 arguments.callee.caller 来访问相同的信息。

```js
function outer(){
    inner();
}
function inner(){
    // alert(inner.caller);
    alert(arguments.callee.caller);
}
outer();			// 显示 outer() 函数的源代码
```

当函数在严格模式下运行时，访问 arguments.callee 会导致错误。ES 5 还定义了 arguments.caller 属性，但在严格模式下访问它也会导致错误，而在非严格模式下这个属性始终是 undefined。定义这个属性是为了分清 arguments.caller 和函数的 caller 属性。

以上变化都是为了加强这门语言的安全性，这样第三方代码就不能在相同的环境里窥视其他代码了。严格模式还有一个限制：不能为函数的 caller 属性赋值，否则会导致错误。







## 函数属性和方法

ECMAScript 中的函数是对象，因此函数也有属性和方法。

### 属性

每个函数都包含两个属性：length 和 prototype。其中，length 属性表示函数希望接收的命名参数的个数。

```js
function sum(num1, num2){
    return num1 + num2;
}
function sayHi(){
    alert("hi");
}
alert(sum.length); 		// 2
alert(sayHi.length); 	// 0
```

**prototype 属性**

对于 ECMAScript 中的引用类型而言，prototype 是保存它们所有实例方法的真正所在。换句话说，诸如 toString() 和 valueOf() 等方法实际上都保存在prototype 名下，只不过是通过各自对象的实例访问。

在创建自定义引用类型以及实现继承时，prototype 属性的作用是极为重要的。





### apply() 和 call()

call 与 apply 都属于 Function.prototype 的一个方法，所以每个 function 实例都有 call、apply 方法。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 this 对象的值，动态改变函数的运行环境（ 执行上下文）。

<u>call() 方法与 apply() 方法的作用相同，只是接收参数的方式不同</u>。

**apply()** 

> *func.apply(thisArg, [argsArray])*

apply() 方法接收两个参数：

- 在其中运行函数的作用域（**上下文**）；
- **参数数组**，数组的每一个成员会依次传递给调用函数。可以是 Array 的实例，也可以是 arguments 对象。<u>通过 apply 可以将数组装换为参数列表的集合</u>。

```js
function sum(num1, num2){
	return num1 + num2;
}
function callSum1(num1, num2){
    // 因为是在全局作用域中调用的，所以传入的 this 就是 window 对象
	return sum.apply(this, arguments); // 传入 arguments 对象
}
function callSum2(num1, num2){
	return sum.apply(this, [num1, num2]); // 传入数组
}
console.log(callSum1(10,10),callSum2(10,10)); 		// 20 20
```

**call()**

> *function.call(thisArg, arg1, arg2, ...)*

对于 call() 方法而言，第一个参数是 this 值没有变化，变化的是其余参数都直接传递给函数。即，传递给函数的参数必须逐个列举出来（参数列表）。



```js
var p1 = {
    name:'小明',
    age:'12',
    action:function(where,doing){
        console.log(this.age + '岁的'+this.name + '在'+ where + doing);
    } 
}
var p2 = {
    name:'小红',
    age:'15'
}
console.log(p1.action.call(p2,'操场上','运动'));	// 15岁的小红在操场上运动
```

传递参数并非 apply() 和 call() 真正的用武之地；它们真正强大的地方是能够扩充函数赖以运行的作用域。使用 call()（或 apply()）来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。

```js
window.color = "red";
var o = { color: "blue" };

function sayColor(){
    alert(this.color);
}
sayColor(); 			// red
sayColor.call(this); 	// red
sayColor.call(window); 	// red
sayColor.call(o); 		// blue，
// 对比之前的例子 o.sayColor = sayColor; o.sayColor(); 
```

如果 apply() 和 call() 处于非严格模式下，指定为 `null` 或 `undefined` 时会自动替换为指向全局对象，原始值会被包装。





### **bind()**

> *function.bind(thisArg[, arg1[, arg2[, ...]]])*

ES 5 还定义了 bind() 方法，这个方法会创建一个函数的实例，其 this 值会被绑定到传给 bind() 函数的值。bind() 函数会创建一个新的绑定函数（bound function，BF）。绑定函数是一个 怪异函数对象，它包装了原函数对象。调用**绑定函数**通常会导致执行**包装函数**。

返回一个原函数的拷贝，并拥有指定的 **`this`** 值和初始参数。用法：

```js
const newFun = fun.bind(thisArg, arg1, arg2, ...);
newFun();
```

支持 bind() 方法的浏览器有 IE9+、Firefox 4+、Safari 5.1+、Opera 12+ 和 Chrome。

```js
window.color = "red";
var o = { color: "blue" };
function sayColor(){
    alert(this.color);
}
// sayColor() 调用 bind() 并传入对象 o，创建了 objectSayColor() 函数。
var objectSayColor = sayColor.bind(o);
objectSayColor(); // blue。objectSayColor() 函数的 this 值等于 o
```



为每一个指定元素的指定事件绑定一个事件处理器函数，可是使用 `bind(type)` 实现。







手写 bind

bind 有如下三个功能点：

- 改变原函数的 this 指向，即绑定上下文，返回原函数的拷贝
- 当绑定函数被调用时，bind 的额外参数将置于实参之前传递给被绑定的方法。
- 注意，一个绑定函数也能使用 new 操作符创建对象。new 操作符修改 this 指向的优先级更高。

```js
Function.prototype.myBind = function(thisArg) {
    if (typeof this !== 'function') {
        return
    }
    var _self = this
    // 从第二个参数截取
    var args = Array.prototype.slice.call(arguments, 1)
    // 定义一个空函数
    var fnNop = function () {} 
    var fnBound = function () {
        // 检测 New
    	// 如果当前函数的 this 指向的是构造函数中的 this 则判定为 new 操作
        var _this = this instanceof _self ? this : thisArg;
        return _self.apply(_this, args.concat(Array.prototype.slice.call(arguments)))
    }
    // 维护原型关系
    if (this.prototype) {
        fnNop.prototype = this.prototype;		// 有问题？
    }
  	// 为了完成 new 操作，还需要执行原型链接
    fnBound.prototype = new fnNop();
    return fnBound;
}
```

另一种实现方法

```js
Function.prototype.myBind = function (context, ...args) {
    const fn = this;
    args = args ? args : [];
    return function newFn(...newFnArgs) {
        if (this instanceof newFn) {
            return new fn(...args, ...newFnArgs);
        }
        return fn.apply(context, [...args,...newFnArgs]);
    }
}
```







bind,apply,call

相似点：

- 都可以用来改变 this 的指向。
- 第一个参数都是 this 要指向的对象。
- 都可以利用后续参数传参。

不同之处：

- bind 和 call 从第二个参数开始接受的是参数列表；而 apply 第二个参数是一个数组。

- call()、apply() 可以看做是某个对象的方法，通过调用方法的形式来间接的调用函数。bind() 就是将某个函数绑定到某个对象上。

- apply 和 call 调用有指定 `this` 值和参数的函数的结果。若该方法没有返回值，则返回 `undefined`。bind 返回一个原函数的拷贝，并拥有指定的 **`this`** 值和初始参数。

- apply，call 是立即调用；bind 返回对应的函数，便于稍后调用，而不是直接执行函数。

- 在 ES6 的箭头函数下, call 和 apply 将失效。对于箭头函数来说，箭头函数体内的 this 对象，就是定义时所在的对象，而不是使用时所在的对象

  



 












手写原生 apply 实现

```js
// 第一步：在 Function 原型上扩展新方法，并接收 2 个参数
Function.prototype.myApply = function (context, args) {
    // 第二步：容错处理。默认为 window，也可以用 ES6 给参数设置默认参数
    context = context || window
    args = args ? args : [];
    // 第三步：使用隐式绑定去实现显式绑定
    // 给 context 新增一个独一无二的属性以免覆盖原有属性
    const key = Symbol();
    context[key] = this;
    const result = context[key](...args);	// 通过隐式绑定的方式调用函数
    // 第四步：返回函数调用的返回值，并且删除 context上的属性
    delete context[key];		// 删除添加的属性
    return result;				// 返回函数调用的返回值
}
```



手写原生 call 实现

```js
// 实现与 apply 类似，只是传递参数的形式不同
// ...扩展运算符可以用 arguments 代替
Function.prototype.myCall = function (context, ...args) {
    context = context || window;
    args = args ? args : [];
    const key = Symbol();
    context[key] = this;
    const result = context[key](...args);
    delete context[key];
    return result;
}
```







### 继承方法

每个函数继承的 toLocaleString() 和 toString() 方法始终都返回函数的代码。返回代码的格
式则因浏览器而异——有的返回的代码与源代码中的函数代码一样，而有的则返回函数代码的内部表示，即由解析器删除了注释并对某些代码作了改动后的代码。由于存在这些差异，我们无法根据这两个方法返回的结果来实现任何重要功能；不过，这些信息在调试代码时倒是很有用。另外一个继承的 valueOf() 方法同样也只返回函数代码。







# 参考资料

[this、apply、call、bind - 掘金](https://juejin.im/post/59bfe84351882531b730bac2)

[前端面试之手写一个bind方法 - CSDN](https://blog.csdn.net/q3254421/article/details/82999718)

[JavaScript 参考 函数 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions)

[JavaScript 指南 函数 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions)

[JavaScript 秘密花园](http://bonsaiden.github.io/JavaScript-Garden/zh/#function.general)