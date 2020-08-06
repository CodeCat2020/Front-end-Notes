# 函数表达式

函数表达式的语法：

```js
var/let function_expression = function [name]([param1[, param2[, ..., paramN]]]) {
   statements
};		// 函数末尾有一个分号
```

- `name`：函数名称。可被省略，此种情况下的函数是匿名函数（*anonymous*）。 函数名称只是函数体中的一个本地变量。
- `paramN`：被传递给函数的一个参数名称。一个函数至多拥有 255 个参数。
- `statements`：构成函数体的语句。

从 [ES2015](https://developer.mozilla.org/zh-CN/docs/) 开始，也可以使用[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions) 。



被函数表达式赋值的那个变量会有一个 name 属性。

- 如果把这个变量赋值给另一个变量，这个 name 属性的值不会改变。
- 如果函数是匿名函数，name 属性的值就是被赋值的变量的名称（隐藏值）。这对于[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)也同样适用（箭头函数没有名字，所以只能赋予 name 属性一个隐性名）。
- 如果函数不是匿名的话，name 属性的值就是这个函数的名称（显性值）。

```js
var foo1 = function() {}			// 匿名函数
console.log(foo1.name);	 	// "foo1"
var foo2 = foo1						// 赋值给另一个变量
console.log(foo2.name); 	// "foo1"
var bar = function baz() {}			// 命名函数表达式
console.log(bar.name); 		// "baz"

console.log(foo1 === foo2); // true
console.log(typeof baz);	// undefined
console.log(bar === baz); 	// ReferenceError: baz is not defined
```





函数表达式的作用

- 递归

- IIFE（即时调用的函数表达式），它一旦定义就运行。



## 匿名函数

没有名字的函数表达式也叫做匿名函数（也称为拉姆达函数）。匿名函数中，function 关键字后面没有标识符。

```js
var functionName = function(arg0, arg1, arg2){
	// 函数体
};
```



匿名函数有很多作用，赋予一个变量则创建函数，赋予一个事件则成为事件处理程序或创建闭包等等。



## 命名函数表达式

有函数名的函数表达式叫做命名函数表达式（Named function expression）。将命名函数赋值给一个变量。

```js
var functionName = function name(arg0, arg1, arg2){
	// 函数体
};
```

函数名称将会且只会作为函数体（作用域内）的本地变量。

下例中，`bar` 在函数体外是不可见的，这是因为已经把函数赋值给了 `foo`； 然而在函数体内部依然可见。这是由于 JavaScript 的 [命名处理](http://bonsaiden.github.io/JavaScript-Garden/zh/#function.scopes) 所致， 函数名在函数内*总是*可见的。

**注意：**在 IE8 及 IE8 以下版本浏览器 `bar` 在外部也是可见的，因为浏览器对命名函数赋值表达式进行了错误的解析， 解析成两个函数 `foo` 和 `bar`。

```js
var foo = function bar() {
    bar(); 	// 正常运行
}
bar(); // 出错：ReferenceError
```

命名函数表达式可以用于在函数内部代指其本身，或者在调试器堆栈跟踪中识别该函数。





## 递归

一个函数可以指向并调用自身。调用自身的函数称之为*递归函数*。有三种实现方法：

- 函数名：函数名可能会发生变化。

- `arguments.callee`：一个指向正在执行的函数的指针。在 ES5 严格模式下，不能通过脚本访问这个属性，否则会导致错误。

- 作用域下的一个指向该函数的变量名

  ```js
  var foo = function bar() {
      // 实现递归，以下的语句是等价的
  	bar();					// 函数名
      arguments.callee();		// 内部属性
      foo();					// 命名函数表达式
  };
  ```



以经典的递归阶乘函数为例。arguments.callee 可以解决函数名改变问题。

```js
function factorial(num){
    if (num <= 1){
    	return 1;
    } else {
    	// return num * factorial(num-1);		// 函数名可能会发生变化
        return num * arguments.callee(num-1);	// 严格模式下，不能访问
    }
}
```

命名函数表达式可以在 ES5 严格模式下实现递归。

```js
var factorial = (function f(num){
    if (num <= 1){
    	return 1;
    } else {
    	return num * f(num-1);
    }
});
```



## 立即执行函数



**什么是立即执行函数**

当函数只使用一次时，通常使用 IIFE （Immediately Invokable Function Expressions，立即执行函数）。**IIFE** 是在函数声明后立即调用的函数表达式。

```js
(function() {
    statements
})();
```

在函数体后面加括号就能立即调用。而这个函数必须是函数表达式，不能是函数声明（函数声明后面不能跟圆括号）。这意味着不能以 function 关键字开头，因为 JavaScript 将 function 关键字当作一个函数声明的开始。

```js
function(){console.log('Hello world')}()
// SyntaxError: Function statements require a function name
```

在 function 前面加括号、 `!`、`+`、` -` 、`,` 等，可以告诉 JavaScript 引擎这是一个函数表达式，通过语法检查。加括号是最安全的做法，因为其它运算符可能会和函数的返回值进行运算，造成不必要的麻烦。

```js
(function(a){ console.log(a); })(123);	// 输出123,用括号把整个表达式包起来
(function(a){ console.log(a); }(1234));	// 输出1234，用括号把函数包起来
// 括号之外的符号，不在意值是多少，只想通过语法检查。
!function(a){ console.log(a); }(12345);		// 输出12345,使用 ！运算符
+function(a){ console.log(a); }(123456);	// 输出123456,使用 + 运算符
-function(a){ console.log(a); }(1234567);	// 输出1234567,使用 - 运算符
~function(){console.log('我是匿名函数')}()
var fn = function(a){  console.log(a);}(12) // 输出12，使用 = 运算符  
void function(){console.log('Hello')}()
new function(){console.log('Hi')}()
```



立即执行函数有什么用？

- 创建一个独立的作用域，执行完毕就销毁自身定义的变量，外面访问不到这个作用域里面的变量，可以避免变量污染。
  - 模仿块作用域，减少闭包占用的内存问题
  - 限制向全局作用域中添加过多的变量和函数
- 闭包和私有数据。





模仿块级作用域

ES5 没有块级作用域的概念，在块语句中定义的变量，实际上是在包含函数中而非语句中创建的。立即执行函数可以模仿块级作用域。

在函数内部，这种做法可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。只要函数执行完毕，就可以立即销毁其作用域链了。

```js
function outputNumbers(count){
    (function () {
        for (var i = 0; i < count; i++){
            alert(i);
        }
    })();
    alert(i); //导致一个错误！
}
```

在全局作用域中，使用立即执行函数可以限制向全局作用域中添加过多的变量和函数。

过多的全局变量和函数很容易导致命名冲突。而通过创建私有作用域，每个开发人员既可以使用自己的变量，又不必担心搞乱全局作用域。例如：

```js
(function(){
    var now = new Date();		// 局部变量，不必在全局作用域中创建它。
    if (now.getMonth() == 0 && now.getDate() == 1){
        alert("Happy new year!");
    }
})();
```





# 闭包



## 什么是闭包

闭包（closure）是指<u>有权访问另一个函数作用域中的变量的函数</u>。创建闭包的常见方式，就是<u>在一个函数内部创建另一个函数</u>。

下例中，f2() 被包含在 f1() 中，  f1() 的所有局部变量，对 f2() 都是可见的，但是 f2() 的所有局部变量，对 f1() 不可见。

```js
function f1(){
    var a = 999;
    function f2(){
        var b = 666;
        console.log(a); 		// 999
    }
    f2();
    //console.log(b);	// ReferenceError: b is not defined
}
f1();
```



**闭包需要返回函数吗？**

不需要

**闭包与匿名函数的关系**

闭包可以用函数声明，也可以用函数表达式定义。因此，闭包不一定都是匿名函数，匿名函数不一定是闭包。



**如何从外部读取局部变量？**

当在函数内部定义了其他函数时，就创建了闭包。闭包有权访问包含函数内部的所有变量，原理如下。

- 在后台执行环境中，闭包的作用域链包含着它自己的作用域、包含函数的作用域和全局作用域。
- 通常，函数的作用域及其所有变量都会在函数执行结束后被销毁。
- 但是，当函数返回了一个闭包时，这个函数的作用域将会一直在内存中保存到闭包不存在为止。



## 闭包原理





## 闭包的作用

- 递归，斐波那契数列
- ES5 模拟块作用域











## 闭包的优点和缺点



内部函数可以引用外层的参数和变量。

参数和变量不会被垃圾回收机制回收。



闭包有 3 个特性。

- 函数嵌套函数。
- 在函数内部可以引用外部的参数和变量。
- 参数和变量不会以垃圾回收机制回收。



闭包的优点：1.能够读取函数内部的变量2.让这些变量一直存在于内存中，不会在调用结束后，被垃圾回收机制回收    

​    闭包的缺点：正所谓物极必反，由于闭包会使函数中的变量保存在内存中，内存消耗很大，影响网页性能。    

​     所以不能滥用闭包，解决办法是，退出函数之前，将不使用的局部变量删除。简单的说就是把那些不需要的变量，但是垃圾回收又收不走的的那些赋值为null，然后让垃圾回收走；



使用闭包的注意点

1）由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

2）闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。







## 闭包与变量

作用域链的配置机制的副作用：闭包只能取得包含函数中任何变量的最后一个值。闭包保存的是整个变量对象，而不是某个特殊的变量。

下例中，createFunctions() 返回一个函数数组，期待结果是每个函数返自己的索引值，但实际上每个函数都返回 10。每个函数的作用域链中都保存着 createFunctions() 函数的活动对象， 所以它们引用的是同一个变量 i 。当 createFunctions() 函数返回后，变量 i 的值是 10。

```js
function createFunctions(){
    var result = new Array();
    for (var i = 0; i < 10; i++){
        // result[i] = i;	// [0, 1, 2, 3, 4,  5, 6, 7, 8, 9]
        result[i] = function(){
            return i;	  // 返回一个长度为 10 的函数数组，每个函数都返回 10
        };
    }
    return result;
}
console.log(createFunctions());
// [[Function],[Function], [Function],[Function],[Function], [Function],[Function],[Function], [Function],[Function]]
```

可以通过**立即执行函数**强制让闭包的行为符合预期。下例中，没有直接把闭包赋值给数组，而是定义了一个匿名函数，并将立即执行该匿名函数的结果赋给数组。

```js
function createFunctions(){
    var result = new Array();
    for (var i = 0; i < 10; i++){
        result[i] = function(num){		// 匿名函数
            return function(){
                return num;				// 返回各自不同的索引值
            };
        }(i);
    }
    return result;
}
```

如果浏览器支持 ES6，也可以将 for 循环中的 var 换成 let，使用块级作用域解决。







```js
function foo() {
    var i = 0;
    return function() {
        console.log(i++);
    }
}
var f1 = foo(),
    f2 = foo();
f1();		// 0
f1();		// 1
f1();		// 1
f2();		// 0
f2();		// 0
```

一般来说函数执行完后它的局部变量就会随着函数调用结束被销毁，但是此题foo函数返回了一个匿名函数的引用（即一个**闭包**），它可以访问到foo()被调用产生的环境，而局部变量i一直处在这个环境中，只要一个环境有可能被访问到，它就不会被销毁，所以说闭包有延续变量作用域的功能。





## 关于 this 对象

this 对象是在运行时基于函数的执行环境绑定的。**在全局函数中，this 等于window**，而当函数被作为某个对象的方法调用时，this 等于那个对象。

匿名函数的执行环境具有全局性，因此其 this 对象通常指向 window。

```js
var name = "The Window";		// 全局变量 name
var object = {
    name : "My Object",			// 创建一个 name 属性
    getNameFunc : function(){	// 创建一个方法
        return function(){		// 方法返回一个匿名函数
        	return this.name;
        };
    }
};
alert(object.getNameFunc()()); // "The Window"（在非严格模式下）
```

把外部作用域中的 this 对象保存在一个闭包能够访问到的变量里，可以让闭包访问该对象。

```js
var name = "The Window";
var object = {
    name : "My Object",
    getNameFunc : function(){
        var that = this;			// 保存外部作用域的 this 对象
        return function(){
            return that.name;
        };
    }
};
alert(object.getNameFunc()()); // "My Object"
```

arguments 也存在同样的问题。如果想访问作用域中的 arguments 对象，必须将对该对象的引用保存到另一个闭包能够访问的变量中。

在几种特殊情况下，this 的值可能会意外地改变。

```js
var name = "The Window";
var object = {
    name : "My Object",
    getName: function(){	// getName() 方法只简单地返回 this.name 的值
        return this.name;	// 没有 this 会报错
    }
};
console.log(
    object.getName(); 			// "My Object"，this.name 就是 object.name。
    (object.getName)(); 		// "My Object"
	(object.getName = object.getName)(); // "The Window"，在非严格模式下
	// 先执行赋值语句，然后再调用结果。赋值表达式的值是函数本身，this 的值不能得到维持
);
var func = object.getName;		// func 的运行环境是全局，因此 this 指向全局对象
console.log(func()); 			// The Window
```





## 内存泄漏

如果闭包的作用域链中保存着一个 HTML 元素，那么就意味着该元素将无法被销毁。

下例中，由于匿名函数保存了一个对 assignHandler() 的活动对象的引用，只要匿名函数存在，element 的引用数至少也是 1，因此它所占用的内存就永远不会被回收。

```js
function assignHandler(){
    var element = document.getElementById("someElement");
    element.onclick = function(){
        alert(element.id);		// 循环引用
    };
}
```

这个问题可以通过稍微改写一下代码来解决。

通过把 element.id 的一个副本保存在一个变量中，并且在闭包中引用该变量消除了循环引用。**闭包会引用包含函数的整个活动对象**，而其中包含着 element。即使闭包不直接引用 element，包含函数的活动对象中也仍然会保存一个引用。因此，有必要把 element 变量设置为 null，解除对 DOM 对象的引用，确保正常回收其占用的内存。

```js
function assignHandler(){
    var element = document.getElementById("someElement");
    var id = element.id;		// 把 element.id 的一个副本保存在一个变量中
    element.onclick = function(){
        alert(id);		// 在闭包中引用该变量消除了循环引用
    };
    element = null;		// 解除对 DOM 对象的引用
}
```







## 私有变量

任何在函数中定义的变量，都可以认为是私有变量，因为不能在函数的外部访问这些变量。私有变量包括函数的参数、局部变量和在函数内部定义的其他函数。

```js
function add(num1, num2){
    var sum = num1 + num2;	
    return sum;			// 有3 个私有变量：num1（形参）、num2（形参）和sum（局部变量）。
}
```

如果在这个函数内部创建一个闭包，那么闭包通过自己的作用域链也可以访问这些变量。而利用这一点，就可以创建用于访问私有变量的公有方法。

把有权访问私有变量和私有函数的公有方法称为特权方法（privileged method）。

可以使用构造函数模式、原型模式来实现自定义类型的特权方法，也可以使用模块模式、增强的模块模式来实现单例的特权方法。

### 构造函数

第一种是在构造函数中定义特权方法。利用私有和特权成员，可以隐藏那些不应该被直接修改的数据。

```js
function Person(name){		// 构造函数
    // 私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    // 特权方法
    this.publicMethod = function (){
        privateVariable++;
        return privateFunction();
    };
    // 特权方法（闭包）
    this.getName = function(){
        return name;
    };
    // 特权方法（闭包）
    this.setName = function (value) {
        name = value;
    };
}
// 在创建 Person 的实例后，只能通过特权方法直接访问私有变量和私有函数
var person = new Person("Nicholas");
alert(person.getName()); 		// "Nicholas"
person.setName("Greg");
alert(person.getName()); 		// "Greg"
```

但是必须使用构造函数模式创建对象，构造函数针对每个实例都会创建同样一组新方法，有大量的重复代码。使用静态私有变量来实现特权方法就可以避免这个问题。



### 静态私有变量

通过在私有作用域中（立即执行函数）定义私有变量或函数，也可以创建特权方法。

这个模式与在构造函数中定义特权方法的主要区别就在于，**私有变量和函数是由实例共享的**。由于
特权方法是在原型上定义的，因此所有实例都使用同一个函数。而这个特权方法，作为一个闭包，总是保存着对包含作用域的引用。

以这种方式创建静态私有变量会因为使用原型而增进代码复用，但每个实例都没有自己的私有变量。

```js
(function(){
    // 私有变量和私有函数
    var name = "";
    // 构造函数
    Person = function(value){	// Person 函数表达式，初始化但未经声明，是一个全局变量
        name = value;
    };
    // 公有/特权方法
    Person.prototype.getName = function(){
        return name;
    };
    Person.prototype.setName = function (value){
        name = value;
    };
    // 变量 name 变成了一个静态的、由所有实例共享的属性。
})();
var person1 = new Person("Nicholas");
console.log(person1.getName()); 		// "Nicholas"
var person2 = new Person("Michael");
console.log(person1.getName());  		// "Michael"
person1.setName("Greg");
console.log(person1.getName());  		// "Greg"
console.log(person2.getName());  		// "Greg"，所有实例都会返回相同的值。
```



### 模块模式

道格拉斯所说的模块模式（module pattern）为单例创建私有变量和特权方法。单例（singleton），指的就是只有一个实例的对象。按照惯例，JavaScript 是以对象字面量的方式来创建单例对象的。

```js
var singleton = {
    name : value,
    method : function () {
        //这里是方法的代码
    }
};
```

模块模式通过为单例添加私有变量和特权方法能够使其得到增强，其语法形式如下：

```js
var singleton = function(){
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    //特权/公有方法和属性
    return {
        publicProperty: true,
        publicMethod : function(){
            privateVariable++;
            return privateFunction();
        }
    };
}();
```



### 增强的模块模式

在返回对象之前加入对其增强的代码。

增强的模块模式适合：单例必须是某种类型的实例，同时还必须添加某些属性和（或）方法对其加以增强的情况。

```js
var singleton = function(){
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false;
    }
    //创建对象
    var object = new CustomType();
    //添加特权/公有属性和方法
    object.publicProperty = true;
    object.publicMethod = function(){
        privateVariable++;
        return privateFunction();
    };
    //返回这个对象
    return object;
}();
```





# 参考资料

[学习Javascript闭包（Closure） - 阮一峰](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)

[JavaScript 参考 函数表达式 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/function)

[JavaScript 指南 函数 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions)

[深入理解javascript中的立即执行函数(function(){…})()](https://www.jb51.net/article/50967.htm)

[「每日一题」什么是立即执行函数？有什么作用？ - 知乎](https://zhuanlan.zhihu.com/p/22465092)

[详解立即执行函数(function(){}()),(function(){})()](https://www.cnblogs.com/jdWu-d/p/11587805.html)

[什么是立即执行函数，它有什么作用？ - 简书](https://www.jianshu.com/p/b10b6e93ddec)

[JavaScript 秘密花园](http://bonsaiden.github.io/JavaScript-Garden/zh/#function.general)

