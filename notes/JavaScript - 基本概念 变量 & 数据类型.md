# 变量

从字面上看，变量是可变的量；从编程角度讲，变量是用于存储某种/某些数值的存储器。

ECMAScript 的变量是松散类型的，可以用来保存任何类型的数据。换句话说，每个变量仅仅是一个用于保存值的占位符而已。

可以把 ECMAScript 变量看做一个盒子，盒子用来存放物品，物品可以是衣服、玩具、水果...等。

## **声明 & 初始化**

定义变量时要使用 var 操作符，后跟变量名（即一个标识符）。

```js
var message;	// 定义一个名为 message 的变量
```

支持直接初始化变量。

```js
var message = "hi";
```

可以在修改变量值的同时修改值的类型。

```js
var message = "hi";
message = 100; 	// 有效，但不推荐
```

用逗号分隔开使用一条语句定义多个变量，初始化或不初始化均可：

```js
var message = "hi",
found = false,
age = 29;
```

在严格模式下，不能定义名为 eval 或 arguments 的变量，否则会导致语法错误。

在严格模式下，初始化未经声明的变量会导致错误。建议在初始化变量之前，先声明变量。



## 变量提升



### 定义

变量提升（hoisting）：函数及变量的声明总是会被解释器悄悄地被"提升"到方法体的最顶部。

变量提升的意思是在执行代码之前会先读取函数及变量声明。这就意味着可以把函数声明和变量声明放在调用它们的语句后面。

- JavaScript 只有声明的 var 变量会提升，初始化的不会，直接赋值的也不会。let、const 变量没有变量提升。

  ```js
  var b = 5;				// 初始化
  console.log("a:"+a); 	// a:undefined。变量 a 提升，赋值在后面
  console.log("b:"+b); 	// b:5
  var a = 1; 		
  console.log("a:"+a);	// a:1
  //console.log("c:"+c); 	// ReferenceError: c is not defined
  c = 2;
  console.log("c:"+c); 	// c:2
  ```

  

- **只有函数声明才有变量提升**，函数表达式没有变量提升。

```js
function myFunc() {
    console.log("func1():"+func1()); // func1():2
    function func1() {
        return 2;
    }
    console.log("func2():"+func2); // func2():undefined
    var func2 = function(){
		console.log(func2);
	}
    console.log("func2():"+func2); // function(){console.log(func2);}
}
myFunc();
```

**提升的优先级**

函数声明的优先级高于变量声明的优先级，并且函数声明和函数定义的部分一起被提升。

函数声明不会被变量声明覆盖，但是在变量赋值之后会被覆盖。

```js
console.log(typeof a);	// 输出 function
console.log(a);			// [Function: a]，会执行函数 a 中的console.log。
console.log(a());		// undefined，函数没有返回值
var a = 10;
function a(){}
console.log(typeof a);	// 输出 number，如果变量a没有赋值，仍会输出 function
//console.log(a());		// TypeError: a is not a function
a = 6;
console.log(a);			// 6
console.log(a());		// TypeError: a is not a function
```



### 原因



JavaScript 在编译过程中的词法分析阶段就已经分析出当前作用域内的相关变量，并且在词法分析阶段就把它们挂载到了词法环境或变量环境上。所以不管是 let，const 还是 var 声明的变量都存在变量提升的过程，只不过 let 和 const 定义的变量在执行之前是不可访问的而已。

变量提升是执行上下文的小把戏，而不会修改源代码。在执行任何语句之前，解释器要从创建执行上下文后已经存在的作用域（scope ）中找到变量的值。

详细内容见 **[JavaScript 语言类型 & 运行机制](./JavaScript%20-%20运行机制.md) 变量提升**。



### 避免

**避免变量提升**

为了避免这些问题，通常在每个作用域开始前声明这些变量，这也是正常的 JavaScript 解析步骤，易于理解。

- 使用严格模式。严格模式不允许使用未声明的变量。
- 







# 数据类型



ECMAScript 不支持任何创建自定义类型的机制，而所有值最终都将是下述数据类型之一。ECMAScript 6 标准定义了 8 种内置数据类型：

- 七种基本/原始/简单数据类型：
  1. **Undefined** ，一个特殊关键字，表示变量未定义时的属性。
  2. **Null** ， 一个表明 null 值的特殊关键字。
  3. **Boolean**，有 2 个值分别是：`true` 和 `false`。
  4. **Number**，整数或浮点数，例如： `42` 或者 `3.14159`。
  5. **String**，一串表示文本值的字符序列，例如："Howdy" 。
  6. 任意精度的整数 (BigInt) ，可以安全地存储和操作大整数，甚至可以超过数字的安全整数限制。
  7. Symbol，实例是唯一且不可改变。（ES 6）
- Object，对象，本质上是由一组无序的名值对组成的。

**容易混淆的地方**：

- 内置数据类型和内置引用类型容易混淆。一个 JavaScript 变量肯定是内置数据类型中的一种，所有的引用类型肯定是 object 类型。
- 这里的数据类型容易与变量类型混淆。根据变量包含的值的类型，变量可以分为基本类型（数据段）和引用类型（对象）。



## **Undefined 类型**

Undefined 类型只有一个值：undefined。在使用 var 声明变量但未对其加以初始化时，这个变量的值就是 undefined。

```js
var message;
alert(message == undefined); //true

var message = undefined;	// 没必要，因为未经初始化默认为 undefined 
alert(message == undefined); //true
```

undefined 的用法

- 变量被声明了，但没有赋值时，就等于 undefined。
- 调用函数时，应该提供的参数没有提供，该参数等于 undefined。
- 对象没有赋值的属性，该属性的值为 undefined。
- 函数没有返回值时，默认返回 undefined。

什么是未声明和未初始化的变量？

未声明的变量指程序中不存在且未声明的变量。未初始化的变量指在程序中声明但尚未给出任何值的变量。

如果程序尝试读取未声明变量的值，则会在运行时遇到错误。如果程序尝试读取未初始化的变量的值， 则返回 undefined。

```js
var message; 	// 变量声明之后默认取得了 undefined 值
alert(message); // "undefined"
alert(age); 	// 报错。age 并没有声明，也没有初始化
```

对于尚未声明过的变量，只能执行一项操作，即使用 typeof 操作符检测其数据类型（对未经声明的变量调用 delete 不会导致错误，但这样做无实际意义，而且在严格模式下确实会导致错误）。

对未初始化的变量执行 typeof 操作符会返回 undefined 值，而对未声明的变量执行 typeof 操作符同样也会返回 undefined 值。**显式地初始化变量可以区分未声明和未初始化**。

```js
var message; 	// 变量声明之后默认取得了undefined 值
alert(typeof message); // "undefined"
alert(typeof age); 		// "undefined"，这个变量并没有声明
```





## **Null 类型**



Null 类型也只有一个值：null。从逻辑角度来看，**null 值表示一个空对象指针**，使用 typeof 操作符检测 null 值时会返回"object"。

```js
var car = null;
alert(typeof car); // "object"
```

如果定义的变量将用于保存对象，那么最好将该变量初始化为 null。只要直接检查 null 值就可以知道相应的变量是否已经保存了一个对象的引用。

```js
if (car != null){
	// 对 car 对象执行某些操作
}
```

### Undefined vs Null

因为 undefined 值派生自 null 值，因此 ECMA-262 规定对它们的相等性测试要返回  true：

```js
alert(null == undefined); // true
```



null 和 undefined 的区别是什么？

相同点：转换为 Boolean 类型时，都会被自动转为 false。

- 本质： null 是一个表示“无”的对象；undefined 是一个表示“无”的原始值。undefined 派生自 null。
- 转为数值： null 转为数值时为 0；undefined 转为数值时为 NaN。
- 表示意义：null 用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。当声明的变量还未初始化时，变量的默认值为 undefined。

- 无论在什么情况下都没有必要把一个变量的值显式地设置为 undefined，可是同样的规则对 null 却不适用。只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 null 值。这样做不仅可以体现 null 作为空对象指针的惯例，而且也有助于进一步区分 null 和 undefined。



## **Boolean 类型**

Boolean 类型有两个字面值：true 和 false，区分大小写。并且，true 不一定等于 1，false 也不一定等于 0。

```js
var found = true;
var lost = false;
console.log(found == 1,found === 1,lost == 0,lost === 0);
// true false true false
```



## **Number 类型**

和其他编程语言不同，JavaScript 不区分整数值和浮点数值，所有数字均用浮点数值表示。JavaScript 采用 IEEE 754 标准定义的 **64 位**浮点格式表示数字。——《JavaScript 权威指南》。

JavaScript 数值精度最多可以达到 53 个二进制位（1 个隐藏位与 52 个有效位），相当于 16 个十进制位。

> 疑问：为什么红宝书说“保存浮点数值需要的内存空间是整数值的两倍”，而犀牛书说“JavaScript 不区分整数值和浮点数值，所有数字均用浮点数值表示。JavaScript 采用 IEEE 754 标准定义的 64 位浮点格式表示数字”？（？）



为支持各种数值类型，ECMA-262 定义了不同的数值字面量格式。最基本的数值字面量格式是十进制整数，可以直接在代码中输入：

```js
var intNum = 55; // 整数
```

八进制字面值的第一位必须是 0，然后是八进制数字序列（0～7）。如果字面值中的数值超出范围，那么前导零将被忽略，后面的数值将被当作十进制数值解析。

八进制字面量在严格模式下是无效的，会导致支持的 JavaScript 引擎抛出错误。

```js
var octalNum1 = 070; // 八进制的 56
var octalNum2 = 079; // 无效的八进制数值——解析为 79
```

十六进制字面值的前两位必须是 0x，后跟任何十六进制数字（0～9 及 A～F）。其中，字母 A～F 可以大写，也可以小写。

```js
var hexNum1 = 0xA; // 十六进制的10
var hexNum2 = 0x1f; // 十六进制的31
```

在进行算术计算时，所有以八进制和十六进制表示的数值最终都将被转换成十进制数值。

- X 进制 -> 十进制：整数部分从右往左第 n 个数乘以 X  的 (n-1) 次幂，小数部分从左往右第 n 个数乘以 X 的 -n 次幂，再求和获得十进制数。

- 十六进制 -> 二进制：将 十六进制上每一位分别对应二进制上四位进行转换。

- 二进制 -> 八进制：取三合一

鉴于 JavaScript 中保存数值的方式，可以保存正零（+0）和负零（-0）。正零和负零被认为相等。




### **浮点数值**

浮点数值必须包含一个小数点，并且小数点后必须至少有一位数字。小数点前面可以没有整数，但不推荐。

```js
var floatNum1 = 1.1;
var floatNum2 = 0.1;
var floatNum3 = .1;	 // 有效，但不推荐
```

保存浮点数值需要的内存空间是整数值的两倍（？），因此出现以下情况 ES 会不失时机的将浮点数值转换为整数值：

- 小数点后面没有跟任何数字
- 浮点数值本身表示的就是一个整数

```js
var floatNum1 = 1.; 	// 小数点后面没有数字——解析为1
var floatNum2 = 10.0; 	// 整数——解析为10
console.log(floatNum1,floatNum2);	// 1 10
```

**科学计数法**

```js
var floatNum1 = 3.125e7; // 等于31250000
```

也可以使用 e 表示法表示极小的数值。

```js
var floatNum2 = 3e-17; // 等于0.00000000000000003
```

**计算误差**

浮点数值的最高精度是 17 位小数，但在算术计算中其精确度远远不如整数。

```js
console.log(0.05 + 0.25);		// 0.3
console.log(0.15 + 0.15);		// 0.3
console.log(0.1 + 0.2);			// 0.30000000000000004
```

**产生误差的原因**：二进制浮点数可以精确地表示 1/2、1/8 等，但不能精确地表示 1/10、1/100 等。所以像 0.1 这样的简单数字也不能精确表示。

浮点数值计算会产生舍入误差的问题，是使用基于 IEEE754 数值的浮点计算的通病，其他使用相同数值格式的语言也存在这个问题。

```js
console.log(
    0.1.toString(2),		// 0.0001100110011(无限循环..)
	0.2.toString(2),		// 0.001100110011 (无限循环..)
	(0.1+0.2).toString(2),	
    // 0.0100110011001100110011001100110011001100110011001101
	(0.1+0.2).toString(),	// 0.30000000000000004
);
```

**解决误差**

方法一：toFixed() 方法

toFixed() 方法把 Number 四舍五入为指定小数位数的数字。 

- 语法：`number.toFixed(x)`

- x 规定小数的位数，是 0 ~ 20 之间的值，包括 0 和 20。缺省参数，用 0 代替。
- 返回一个表示数字的字符串，小数点后有固定的 x 位数字

```js
var result1 = (0.2 + 0.4).toFixed(1);
var result2 = parseFloat(result1);
console.log(
    result1,
    typeof result1,
    result2 === 0.6,
);
// 0.6 string true
```

方案二：通用处理方案

把需要计算的数字乘以 10 的 n 次幂，换算成计算机能够精确识别的整数，然后再除以 10 的 n 次幂

```js
formatNum = function(f, digit) { 
    var m = Math.pow(10, digit); 
    return parseInt(f * m, 10) / m; 
} 
var num1 = 0.1; 
var num2 = 0.2;
console.log(formatNum(num1 + num2, 1) === 0.3);
```





### **数值范围**

最小数值：Number.MIN_VALUE，在大多数浏览器中，这个值是 5e-324；

最大数值：Number.MAX_VALUE，在大多数浏览器中，这个值是1.7976931348623157e+308。

Infinity 表示超出 JavaScript 数值范围的数值。Number.NEGATIVE_INFINITY 和 Number.POSITIVE_INFINITY 属性中分别保存着 -Infinity 和 Infinity。

如果某次计算返回了正或负的 Infinity 值，那么该值将无法继续参与下一次的计算。

要想确定一个数值是不是有穷的，可以使用 isFinite() 函数。这个函数在参数位于最小与最大数值之间时会返回 true。

```js
var result = Number.MAX_VALUE + Number.MAX_VALUE;
alert(isFinite(result)); 		//false，变量result的值不在数值范围内
```



### **NaN**

NaN（**Not a Number**，非数值）用于表示一个本来要返回数值的操作数，但未返回数值的情况（这样就不会抛出错误了）。NaN 的数据类型是 Number。

**NaN 的两个特点**

首先，任何涉及 NaN 的操作都会返回 NaN。

```
alert(NaN / 10); // NaN
```

其次，NaN 与任何值都不相等，包括 NaN 本身。

```js
alert(NaN == NaN); //false
```

针对 NaN 的上述两个特点，ECMAScript 定义了 isNaN() 函数。isNaN() 在接收到一个值之后，会尝试将这个值转换为数值。任何不能被转换为数值的值都会导致这个函数返回 true。

```js
alert(isNaN(NaN)); 		// true
alert(isNaN(10)); 		// false（10 是一个数值）
alert(isNaN("10")); 	// false（可以被转换成数值10）
alert(isNaN("blue")); 	// true（不能转换成数值）
alert(isNaN(true)); 	// false（可以被转换成数值1）
```

isNaN() 也适用于对象。在基于对象调用 isNaN() 函数时，首先调用对象的 valueOf() 方法，然后确定该方法返回的值是否可以转换为数值。如果不能，则基于这个返回值再调用 toString() 方法，再测试返回值。而这个过程也是 ECMAScript 中内置函数和操作符的一般执行流程。



isNaN() 判断字符串时会返回 true。所以，判断一个变量是否为 NaN 不能使用 isNaN() 方法。

**根据 NaN 的定义判断**

```js
function isNaN(n) {
    if(typeof(n) === "number" && isNaN(n)) {
        return true;
    } else {
        return false;
    }
}
```

**防止在老版本的浏览器不支持 isNaN() 方法**

```js
if(!Number.isNaN) {
    Number.isNaN = function(n) {
        return( typeof(n) === "number" && window.isNaN(n));
    }
}
```

**利用 NaN 是唯一一个不等于任何自身的特点**

```js
function isNaN(n) {
    if(n !== n) {
        return true;
    } else {
        return false;
    }
}
```

**利用 ES6 中提供的 Object.is() 方法**

```js
console.log(
    Object.is("str", NaN), 		// false
	Object.is(2, NaN), 			// false
	Object.is("str"/2, NaN), 	// true
);
```





## **String 类型**

String 类型用于表示由零或多个 16  位 Unicode 字符组成的字符序列，即字符串。字符串可以由双引号或单引号表示：

```js
var firstName = "Nicholas";
var lastName = 'Zakas';
```

以双引号开头的字符串也必须以双引号结尾，而以单引号开头的字符串必须以单引号结尾。

```js
var firstName = 'Nicholas"; // 语法错误（左右引号必须匹配）
```

### **字符字面量**



String 数据类型包含一些特殊的字符字面量，也叫转义序列，用于表示非打印字符，或者具有其他用途的字符。

| 字面量      | 含义                                                         |
| :---------- | :----------------------------------------------------------- |
| `\0`        | Null 字节                                                    |
| `\b`        | 退格符                                                       |
| `\f`        | 换页符                                                       |
| `\n`        | 换行符                                                       |
| `\r`        | 回车符                                                       |
| `\t`        | Tab (制表符)                                                 |
| `\v`        | 垂直制表符                                                   |
| `\'`        | 单引号                                                       |
| `\"`        | 双引号                                                       |
| `\\`        | 反斜杠字符（\）                                              |
| `\XXX`      | 由从 0 到 377 最多三位八进制数*XXX*表示的 Latin-1 字符。例如，\251 是版权符号的八进制序列。 |
| `\xXX`      | 由从 00 和 FF 的两位十六进制数字XX表示的Latin-1字符。例如，\ xA9是版权符号的十六进制序列。 |
| `\uXXXX`    | 由四位十六进制数字 XXXX 表示的 Unicode 字符。例如，\ u00A9 是版权符号的 Unicode 序列。见[Unicode 转义字符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#String_literals) |
| `\u{XXXXX}` | Unicode 代码点 (code point) 转义字符。例如，\u{2F804} 相当于Unicode 转义字符 \uD87E\uDC04 的简写。 |

这些字符字面量可以出现在字符串中的任意位置，而且也将被作为一个字符来解析。

```js
var text = "This is the letter sigma: \u03a3.";
alert(text.length); // 输出28
```



### **不可变**

ES 中的字符串是不可变的。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量。

```js
var lang = "Java";
lang = lang + "Script";
```

实现这个操作的过程如下：首先创建一个能容纳 10 个字符的新字符串，然后在这个字符串中填充"Java"和"Script"，最后一步是销毁原来的字符串"Java"和字符串"Script"。



## **Object 类型**

对象可以通过执行 new 操作符后跟要创建的对象类型的名称来创建。而创建 Object 类型的实例并为其添加属性和（或）方法，就可以创建自定义对象。

```js
var o = new Object();
```

在 ES 中，如果不给构造函数传递参数，则可以省略后面的那一对圆括号。

```js
var o = new Object; // 有效，但不推荐省略圆括号
```

Object 的每个实例都具有下列属性和方法。

- constructor：保存着用于创建当前对象的函数。

- **hasOwnProperty(propertyName)**：用于检查给定的属性在当前对象实例中是否存在。

  ```js
  obj.hasOwnProperty(prop)
  // prop：要检测的属性的名称（字符串形式）或者 Symbol。
  // 返回值：判断某个对象是否含有特定的自身属性的布尔值 Boolean。
  ```

  注意，此方法无法检查该对象的原型链中是否具有该属性，该属性必须是对象本身的一个成员。

  ```js
  o.hasOwnProperty("name")
  ```

- **isPrototypeOf(object)**：用于检查传入的对象是否是传入对象的原型。允许检查一个对象是否存在于另一个对象的原型链上。

- propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用 for-in 语句来枚举。与 hasOwnProperty() 方法一样，作为参数的属性名必须以字符串形式指定。

- toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应。

- toString()：返回对象的字符串表示。

- valueOf()：返回对象的字符串、数值或布尔值表示。通常与 toString() 方法的返回值相同。

由于在 ES 中 Object 是所有对象的基础，因此所有对象都具有这些基本的属性和方法。









# 类型转换



ECMAScript 数据类型具有动态性。在声明变量时可以不必指定数据类型，而数据类型会在代码执行时会根据需要自动转换。



强制类型转换：容量大的类型转换为容量小的类型。

- 相等和不相等操作符

隐式类型转换的触发场景：

- 当不同数据类型进行相互运算时
  - `+` 运算发生了字符串的隐式转化
  - parseInt() 方法接收一个字符串，并返回一个整数。参数为数字时，隐式转换为字符串。
- 当对非布尔类型的数据求布尔值时
  - 三元运算符，会判断 ? 前的表达式为 true 或者 false。

```js
console.log(
	parseInt(12.34, 10),	// 数字 12.34 隐式转换为 string
	0 ? 1 : 2,				// 0  隐式转换为 false
	1 + '1'					// 数字 1 隐式转换为字符串，+变为字符串拼接
);
// 12 2 11
```



## 转换为 Boolean 类型

ES 中所有类型的值都有与两个 Boolean 值等价的值。

| 数据类型  | 转换为 true 的值             | 转换为 false 的值 |
| --------- | ---------------------------- | ----------------- |
| Boolean   | true                         | false             |
| String    | 任何非空字符串               | ""（空字符串）    |
| Number    | 任何非零数字值（包括无穷大） | **0** 和 NaN      |
| Object    | 任何对象，比如 **[]**。      | **null**          |
| Undefined | n/a                          | **undefined**     |

> n/a（或 N/A），是 not applicable 的缩写，意思是“不适用”。

这些转换规则对理解流控制语句（如 if 语句）自动执行相应的 Boolean 转换非常重要。

```js
var message = "Hello world!";
if (message){	// message 被自动转换成了对应的 Boolean 值（true）。
	alert("Value is true");
}
```





## **非数值→数值**



有 3 个函数可以把非数值转换为数值：转型函数 Number() 可以用于任何数据类型，而 parseInt() 和 parseFloat() 则专门用于把字符串转换成数值。

### Number() 

**Number() 函数**的转换规则如下：

- 如果是 Boolean 值，true 和 false 将分别被转换为 1 和 0。

- 如果是 null 值，返回 0。

- 如果是 undefined，返回 NaN。

- 如果是字符串，遵循下列规则：

  - 整数或浮点数（包括前面带正号或负号的情况），则将其转换为十进制数值，忽略前导零；
  - 字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整数值；
  - 字符串为空（不包含任何字符），则将其转换为 0；
  - 字符串中包含除上述格式之外的字符，则将其转换为 NaN。

- 如果是对象，则调用对象的 valueOf() 方法，然后依照前面的规则转换返回的值。如果转换的结果是 NaN，则调用对象的 toString() 方法，然后再次依照前面的规则转换返回的字符串值。

  ```js
  console.log(
      Number(true),
      Number(false),
      Number(null),
      Number(undefined)
  );
  // 1 0 0 NaN
  console.log(
      Number("-011.2"),
      Number("0xaa"),
      Number(""),
      Number("Hello world!"),
  	Number("123a"),
  );
  // -11.2 170 0 NaN NaN
  console.log(Number(new Object()));		// NaN
  ```



### **parseInt()  函数**

> *parseInt(string, radix)*



由于 Number() 函数在转换字符串时比较复杂而且不够合理，**处理整数**时更常用 parseInt() 函数。parseInt() 函数可解析一个字符串，并返回一个整数。

parseInt() 会忽略字符串前面的空格，直至找到第一个非空格字符。

- 第一个字符不是数字字符或者正负号，返回 NaN。

  ```js
  var num = parseInt(""); 	// 返回 NaN，然而 Number() 返回 0
  ```

- 第一个字符是数字字符，继续解析，直到解析完所有后续字符或者遇到了一个非数字字符。

  ```js
  var num1 = parseInt("1234blue"); // 1234，"blue"会被完全忽略。
  var num2 = parseInt(22.5); 		 // 22，小数点不是有效的数字字符
  ```

- 在 ES 3 中，如果字符串以"0x"开头且后跟数字字符，就会将其当作一个十六进制整数；如果字符串以"0"开头且后跟数字字符，则会将其当作一个八进制数来解析。

  ```js
  console.log(
      parseInt("070"), 	// 56（按八进制数解析）
      parseInt("70"), 	// 70（十进制数）
      parseInt("0xA"), 	// 10（按十六进制数解析）
  	parseInt("0xf"), 	// 15（按十六进制数解析）
  );
  ```
  
- 使用 parseInt() 解析八进制字面量的字符串时，ECMAScript 3 和 5 存在分歧：

  ```js
  // ES 3 认为 070 是 八进制，转换为 56；
  // ES 5 认为 070 是 十进制，前导零无效，转换为 70
  var num = parseInt("070");
  ```

  为了避免错误的解析，可以为这个函数提供第二个参数 radix。可选，表示转换时使用的基数，该值介于 2 ~ 36 之间。

  如果指定了 16 作为第二个参数，字符串可以不带前面的"0x"。

  如果第二个参数为 0，或没有设置该参数时，parseInt() 会根据 string 来判断数字的基数。

  如果 radix 不在 2 ~ 36 之间，并且不为 0，parseInt() 返回 NaN。

  ```js
  console.log(
      parseInt("0xAF", 16),
      parseInt("AF", 16),
      parseInt("AF",0),
      parseInt("AF",1),
      parseInt("12",1),
  ); 
  // 175 175 NaN NaN NaN
  ```

  指定基数会影响到转换的输出结果。建议无论在什么情况下都明确指定基数。

  ```js
  console.log(
      parseInt("11", 2),  // 3 （按二进制解析）
  	parseInt("11", 8),  // 9 （按八进制解析）
  	parseInt("11", 10), // 11 （按十进制解析）
  	parseInt("11", 16), // 17 （按十六进制解析）
  );
  // 3 9 11 17
  ```

解析失败返回 NaN 情况

- radix 数值不合法（不在 2~36 之间，也不是 0）
- string 与 radix 不对应

```js
console.log(
    parseInt("32", 37),	// 基数超出范围
    parseInt("32", 3),	// 基数为 3 时，3 进制中的数由 0、1、2 组成。
); 		
// NaN NaN
```





### **parseFloat()  函数**

> parseFloat(string)

与 parseInt() 函数类似，parseFloat() 也是从第一个字符（位置 0）开始解析每个字符，也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。

```js
console.log(
    parseFloat("1234blue"); 	// 1234 （整数）
    parseFloat("3.125e7"); 		// 31250000
);
```

对于 parseFloat() ，字符串中的第一个小数点是有效的，第二个小数点是无效的。

```js
console.log(
	parseInt(22.5), 			// 22，小数点不是有效的数字字符
	parseFloat("22.5"), 		// 22.5
	parseFloat("22.34.5"), 		// 22.34，第二个小数点无效
);
```

parseFloat() 与 parseInt() 的第二个区别在于它始终都会忽略前导的零。parseFloat() 中，十六进制格式的字符串则始终会被转换成 0。

```js
console.log(
    parseFloat("0908.5"); 	// 908.5
    parseFloat("0xA"); 		// 0
);
```

由于 parseFloat() 只解析十进制值，因此它没有用第二个参数指定基数的用法。

注意：如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后都是零），parseFloat() 会返回整数。

```js
console.log(
    parseFloat("10"),
    parseFloat("10.0"),
	parseFloat("10."),
);
// 10 10 10
```



## **转换为字符串**

### **toString() 方法**

数值、布尔值、对象和字符串值都有 toString() 方法。但 null 和 undefined 值没有这个方法。

```js
var n = 11;
console.log(
	n.toString(),
    true.toString(),
    typeof n.toString(),
	typeof true.toString(),
);
// 11 true string string
```

多数情况下，调用 toString() 方法不必传递参数。但是，在调用数值的 toString() 方法时，可以传递输出数值的基数（2 ~ 36 之间的整数）。若省略该参数，则使用基数 10。

```js
var num = 10;
console.log(
	num.toString(),
    num.toString(2),
    num.toString(8),
	num.toString(16),
);
// 10 1010 12 a
```

###  **String() 函数**

在不知道要转换的值是不是 null 或 undefined 的情况下，还可以使用转型函数 String()，这个函数能够将任何类型的值转换为字符串。String() 函数遵循下列转换规则：

- 如果值有 toString() 方法，则调用该方法（没有参数）并返回相应的结果；
- 如果值是 null，则返回"null"；
- 如果值是 undefined，则返回"undefined"。

```js
var u;
console.log(
	String(10),		// "10"
    String(true),	// "true"
    String(null),	// "null"
    String(u),		// "undefined"
);
```

### 加号操作符

要把某个值转换为字符串，可以使用加号操作符把它与一个字符串（""）加在一起。





# 参考资料

[undefined与null的区别 - 廖雪峰](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html?utm_source=tuicool&utm_medium=referral)