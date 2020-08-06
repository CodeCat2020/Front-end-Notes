# 基本包装类型

有了基本包装类型，JavaScript 中的基本类型值可以被当作对象来访问。三种基本包装类型分别是：Boolean、Number 和 String。以下是它们共同的特征：

- 每个包装类型都映射到同名的基本类型；
- 在读取模式下访问基本类型值时，就会创建对应的基本包装类型的一个对象，从而方便了数据操作；
- 操作基本类型值的语句一经执行完毕，就会立即销毁新创建的包装对象。



## 1. Boolean 类型

Boolean 类型是与布尔值对应的引用类型。

调用 Boolean 构造函数并传入 true 或 false 值，创建 Boolean 对象。

```js
var booObject1 = new Boolean(true);
var booObject2 = new Boolean(false);
console.log(booObject1, booObject2); // [Boolean:true] [Boolean:false]
console.log(typeof booObject1); 	// object
```

对于 Boolean(value)：

- 当作为一个构造函数（带有 new 运算符）调用时，Boolean() 将把它的参数转换成一个布尔值，并且返回一个包含该值的 Boolean 对象。
- 当作为一个普通函数（不带 new 运算符）调用时，Boolean() 只将把它的参数转换成一个原始的布尔值，并且返回这个值。
- 如果省略 value 参数，或者设置为 `0`、`-0`、`null`、`""`、`false`、`undefined` 或 `NaN`，则该对象设置为 false。所有其他值，包括任何对象，空数组（`[]`）或字符串`"false"`，都会创建一个初始值为的对象`true`。
- 对于任何对象，即使是值为 `false` 的 `Boolean` 对象，当将其传给 `Boolean` 函数时，生成的 `Boolean` 对象的值都是 `true`。

不要用创建 `Boolean` 对象的方式将一个非布尔值转化成布尔值，直接将 `Boolean` 当做转换函数来使用即可，或者使用[双重非（!!）运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_Operators#逻辑非（!）)：

```js
var x = Boolean(expression);     // 推荐
var x = !!(expression);          // 推荐
var x = new Boolean(expression); // 不太好
```

Boolean 对象在 ECMAScript 中的用处不大，经常会造成误解。其中最常见的问题就是在布尔表达式中使用 Boolean 对象。建议永远不要使用 Boolean 对象。

```js
var falseObject = new Boolean(false);
var result = falseObject && true;	// falseObject 非空对象，转为 true。
console.log(result, false && true); // true false
```





## 2. Number 类型

Number 是与数字值对应的引用类型。JavaScript的 `Number` 类型为[双精度IEEE 754 64位浮点](https://en.wikipedia.org/wiki/Floating-point_arithmetic)类型。

`Number` 对象由 `Number()` 构造器创建。要创建Number 对象，可以在调用Number 构造函数时向其中传递相应的数值。

```js
var numberObject = new Number(10);
```

`Number` 对象主要用于：

- 如果参数无法被转换为数字，则返回 `NaN`。
- 在非构造器上下文中 (如：没有 `new` 操作符)，`Number` 能被用来执行类型转换。



使用 `Number` 转换 `Date` 对象

```js
var d = new Date("December 17, 1995 03:24:00");
console.log(Number(d));		// 819141840000
```



### 属性

- [`Number.EPSILON`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/EPSILON)：（ES6）两个可表示(representable)数之间的最小间隔。
- [`Number.MAX_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)：（ES6）JavaScript 中最大的安全整数 (`253 - 1`)。
- [`Number.MAX_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_VALUE)：能表示的最大正数。最小的负数是 `-MAX_VALUE`。
- [`Number.MIN_SAFE_INTEGER`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_SAFE_INTEGER)：（ES6）JavaScript 中最小的安全整数 (`-(253 - 1)`)。
- [`Number.MIN_VALUE`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_VALUE)：能表示的最小正数即最接近 0 的正数 (实际上不会变成 0)。最大的负数是 `-MIN_VALUE`。
- [`Number.NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/NaN)：特殊的“非数字”值。
- [`Number.NEGATIVE_INFINITY`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/NEGATIVE_INFINITY)：特殊的负无穷大值，在溢出时返回该值。
- [`Number.POSITIVE_INFINITY`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/POSITIVE_INFINITY)：特殊的正无穷大值，在溢出时返回该值。
- [`Number.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/prototype)：Number 对象上允许的额外属性。



### 方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| isNaN()                                                      | 确定传递的值是否是 NaN。                                     |
| [isFinite](https://www.runoob.com/jsref/jsref-isfinite-number.html) | 检测指定参数是否为无穷大。                                   |
| [`Number.isInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger) | （ES6）确定传递的值类型是“number”，且是整数。                |
| [`Number.isSafeInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/isSafeInteger) | （ES6）确定传递的值是否为安全整数 ( -`(253 - 1)` 至 `253 - 1之间`)。 |
| [toExponential(x)](https://www.runoob.com/jsref/jsref-toexponential.html) | 把对象的值转换为指数计数法。                                 |
| [toFixed(x)](https://www.runoob.com/jsref/jsref-tofixed.html) | 把数字转换为字符串，结果的小数点后有指定位数的数字。         |
| [`Number.toInteger()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toInteger) | （已废弃）计算传递的值并将其转换为整数 (或无穷大)。          |
| [toPrecision(x)](https://www.runoob.com/jsref/jsref-toprecision.html) | 把数字格式化为指定的长度。                                   |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-number.html) | 把数字转换为字符串，使用指定的基数。                         |
| [`Number.parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/parseFloat) | 和全局对象 [`parseFloat()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat) 一样。 |
| [`Number.parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/parseInt) | 和全局对象 [`parseInt()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt) 一样。 |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-number.html) | 返回一个 Number 对象的基本数字值。                           |





**格式化方法**

与 Boolean 类型一样，Number 类型也重写了 valueOf()、toLocaleString() 和 toString()
方法。重写后的 valueOf() 方法返回对象表示的基本类型的数值，另外两个方法则返回字符串形式的数值。可以为 toString() 方法传递一个表示基数的参数。

除了继承的方法之外，Number 类型还提供了一些用于将数值格式化为字符串的方法。

toFixed() 方法会按照指定的小数位返回数值的字符串表示。如果数值本身包含的小数位比指定的多，那么接近指定的最大小数位的值就会舍入。不同浏览器给这个方法设定的舍入规则可能会有所不同。

toFixed() 方法可以表示带有 0 到 20 个小数位的数值。但这只是标准实现的范围，有些浏览器也可能支持更多位数。

```js
var num = 10;
console.log(num.toFixed(2)); 		// "10.00"
console.log((10.005).toFixed(2)); 	// "10.01"
```

toExponential() 按照指定的小数位返回以指数表示法（也称 e 表示法）表示的数值的字符串形式。

```js
var num = 10;
alert(num.toExponential(1)); //"1.0e+1"
```

toPrecision() 方法可能会返回固定大小格式，也可能返回指数格式；具体规则是看哪种格式最合适。这个方法接收一个参数，即表示数值的所有数字的位数（不包括指数部分）。

```js
var num = 99;
alert(num.toPrecision(1)); // "1e+2"。一位数无法准确表示99，向上舍入为 100
alert(num.toPrecision(2)); // "99"
aler t(num.toPrecision(3)); // "99.0"
```







## 3. String 类型

String 类型是字符串的对象包装类型，可以使用 String 构造函数来创建。

String 类型的每个实例都有一个 length 属性，表示字符串中包含多个字符。

```js
var stringObject = new String("hello world");
alert(stringValue.length); 	//"11"
```

String 类型提供了很多方法，用于辅助完成对 ES 中字符串的解析和操作。



### **字符方法**

> *string*.charAt(*index*)

charAt() 和 charCodeAt() 用于访问字符串中特定字符。这两个方法都接收一个参数，即基于 0 的字符位置。前者得到的是字符，后者是字符编码。

  ```js
var stringValue = "hello world";
alert(stringValue.charAt(1)); 		//"e"
alert(stringValue.charCodeAt(1)); 	// 输出"101"，小写字母"e"的字符编码
  ```

ES 5 定义另一种方法 —— 使用方括号加数字索引来访问字符串中的特定字符。这种方法得到了 IE8 及 Firefox、Safari、Chrome 和 Opera 所有版本的支持。如果在 IE7 及更早版本中使用，返回 undefined 值。

  ```js
var stringValue = "hello world";
alert(stringValue[1]); //"e"
  ```

### **字符串操作方法**

#### **concat()**

用于将一或多个字符串拼接起来，不改变原有字符串，返回拼接得到的新字符串。

  ```js
var stringValue = "hello ";
var result = stringValue.concat("world", "!");
alert(result); 			//"hello world!"
alert(stringValue); 	//"hello"，不影响原字符串
  ```



字符串连接方式

在 [JavaScript](http://c.biancheng.net/js/) 中，使用字符串连接有 3 种方式。

- 使用加号运算符

  处理机制：新建一个临时字符串，将新字符串赋值为a+b，然后返回这个临时新字符串同时销毁原始字符串，所以字符串连接效率较低。

- 使用 concat() 方法

- 使用 Array.join() 方法

  在特定的操作环境中，也可以借助数组的 join() 方法来连接字符串，如 HTML 字符串输出等。



1. 在旧浏览器（IE7-）下用 join 会更高效。
2. 在现代浏览器，尽量用"+"，更高效。
3. 少数现代浏览器（如，safari 5.0.5，opera 11.10)， “+” 不一定会比 join 快。
4. 本身是字符串数组的，Array.join() 会更好。
5. 在"+"与 concat 之间，优先使用"+"，方便、直观、高效。







#### **slice()、substr() 和 substring()**

ECMAScript 提供了三个基于子字符串创建新字符串的方法：slice()、substr() 和 substring()。

**相同点：**

这三个方法都不会修改字符串本身的值，返回被操作字符串的一个子字符串，而且也都接受一或两个参数。第一个参数指定子字符串的开始位置，省略第二个参数时，返回从 `start` 开始（包含 `start`）的所有字符。参数全省略时，默认取整个字符串。如果参数为 NaN，将其替换为 0。

- str.slice(beginIndex[, endIndex])
- str.substr(start[, length])
- str.substring(indexStart[, indexEnd])

**不同之处：**

slice() 和 substring() 的第二个参数指定子字符串最后一个字符后面的位置。substr() 的第二个参数指定的是返回的字符个数。

对于 slice() 和 substring() ：

- 返回的内容是从 `start` 开始（包含 `start`）到 `end-1` 处的所有字符，其长度为 `stop-end`。
- 如果 `start` 与 `end` 相等，返回一个空串（即长度为 0 的字符串）。
- 如果 `start` 比 `end` 大， substring() 在提取子串之前会先交换这两个参数。 slice() 返回一个空串。

如果没有给这些方法传递第二个参数或者截取位置大于字符串索引，则将字符串的长度作为结束位置。

  ```js
var stringValue = "hello world";	// 长度为 11 的字符串
console.log(
    stringValue.slice(3),		// "lo world"
    stringValue.substring(3), 	// "lo world"
    stringValue.substr(3), 		// "lo world"
    stringValue,				// "hello world"
    stringValue.slice(3, 7), 	// "lo w"
    stringValue.substring(3,7), // "lo w"
    stringValue.substr(3, 7), 	// "lo worl"
);
  ```

传入负值时，slice() 方法会将传入的负值与字符串的长度相加，substr() 方法将负的第一个参数加上字符串的长度（如果负数绝对值大于字符串长度，参数为 0），而将负的第二个参数转换为 0。最后，substring() 方法会把所有负值参数都转换为 0。

  ```js
var stringValue = "hello world";	
console.log(
    stringValue.slice(-3),	 		// "rld"
    stringValue.substring(-3), 		// "hello world"
    stringValue.substr(-3), 		// "rld"

    stringValue.slice(3, -4), 		// "lo w"
    stringValue.substring(3, -4), 	// "hel"
    stringValue.substr(3, -4), 		// ""（空字符串）
);
  ```

slice 可以用于数组，但另两者不行。



 substr 和 substring 的区别？

相同点：

- 当有一个参数时，两者功能一样，返回从 start 指定的位置直到字符串结束的子串。

不同之处：

- substr() 的第二个参数指定的是返回的字符个数。substring() 的第二个参数指定子字符串最后一个字符后面的位置；
- 传入负值时，substr() 方法将负的第一个参数加上字符串的长度（如果负数绝对值大于字符串长度，参数为 0），而将负的第二个参数转换为 0。substring() 方法会把所有负值参数都转换为 0。
- substr() 方法的第二个参数为 0 或者负数，返回空字符串。substring() 方法两个参数都为 0 或者负数，返回空字符串。
- substring 方法使用 start 和 end 两者中的较小值作为子字符串的起始点。
- IE 的 JavaScript 实现在处理向 substr() 方法传递负值的情况时存在问题，它会回原始的字符串。IE9 修复了这个问题。不建议使用 substr() ，且 ECMAscript 反对使用它。



### **字符串位置方法**

> *string*.indexOf(*searchvalue*,*start*)

indexOf() 和 lastIndexOf() 都是从一个字符串中搜索给定的子字符串，然后返子字符串的位置。如果没有找到该子字符串，则返回 -1。

区别在于：indexOf() 方法从头向后搜索，而 lastIndexOf() 方法从末尾向前搜索。

这两个方法都可以接收一个或两个参数，方法的参数如下表：

| 参数          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| *searchvalue* | 必需。规定需检索的字符串值。                                 |
| *start*       | 可选的整数参数。规定在字符串中开始检索的位置。它的合法取值是 0 到 string Object.length - 1。<br />indexOf() 从该参数指定的位置向后搜索；lastIndexOf() 从指定的位置向前搜索。 |

例子：

  ```js
var stringValue = "hello world";
alert(stringValue.indexOf("o")); 		// 4
alert(stringValue.lastIndexOf("o")); 	// 7
alert(stringValue.indexOf("o", 6)); 	// 7
alert(stringValue.lastIndexOf("o", 6)); // 4
  ```









### **trim()**

这个方法会创建一个字符串的副本（不影响原字符串），删除前置及后缀的所有空格，然后返回结果。

在这个字符串里的空格包括所有的空格字符 (space, tab, no-break space 等)以及所有的行结束符（如 LF，CR）。

  ```js
var stringValue = " hello world ";
var trimmedStringValue = stringValue.trim();
alert(stringValue); 		// " hello world "
alert(trimmedStringValue); 	// "hello world"
  ```

支持这个方法的浏览器有 IE9+、Firefox 3.5+、Safari 5+、Opera 10.5+ 和 Chrome。此外，Firefox 3.5+、Safari 5+ 和 Chrome 8+ 还支持非标准的 trimLeft() 和 trimRight() 方法，分别用于删除字符串开头和末尾的空格。





trim 的实现

```js
String. prototype.trim = function (char, type) {
    if (char) {
        if (type == 'left') {
            // 去除左空格
            return this.replace(new RegExp('^\\' +char+'+', 'g'), '');
        } else if (type == 'right') {
            // 去除右空格
            return this.replace (new RegExp('\\' +char+'+$', 'g'), '');
        }
        return this.replace(new RegExp('^\\' +char+'+|\\' +char+'+$', 'g'), '');
    }
    return this.replace(/^\s+|\s+$/g, '');	// 去除两头空格
}

var str = ' Ruchee ';
console.log(
    // 去除字符串首尾的全部空白
    'xxx' + str.trim() + 'xxx',				// xxxRucheexxx
    // 去除字符串左例空白
    'xxx' + str.trim(' ', 'left') + 'xxx',	// xxxRuchee xxx
    // 去除字符串右侧空白
	'xxx' + str.trim(' ', 'right') + 'xxx'	// xxx Rucheexxx
); 
// xxxRucheexxx xxxRucheexxx xxxRucheexxx
str = '/Ruchee/';
console.log(
    // 去除字符串两例措定字符	
    str.trim('/'),				// Ruchee
    // 去除宇符串左侧指定字符
    str.trim('/', 'left'),		// Ruchee/
    // 去除宇符串右例指定字符
	str.trim('/', 'right'),		// /Ruchee
);
```









### **字符串大小写转换方法**

字符串大小写转换的方法有 4 个：

- toLowerCase()
- toLocaleLowerCase()
- toUpperCase()
-  toLocaleUpperCase()

toLowerCase() 和 toUpperCase() 借鉴自 java.lang.String 中的同名方法。而 toLocaleLowerCase() 和 toLocaleUpperCase() 方法则是针对特定地区的实现。

  ```js
var stringValue = "hello world";
alert(stringValue.toLocaleUpperCase()); // "HELLO WORLD"
alert(stringValue.toUpperCase()); 		// "HELLO WORLD"
alert(stringValue.toLocaleLowerCase()); // "hello world"
alert(stringValue.toLowerCase()); 		// "hello world"
  ```

### **字符串的模式匹配方法**

#### match()

 `match()` 方法检索返回一个字符串匹配正则表达式的的结果。

```
str.match(regexp)
```

语法说明：

- 参数：一个正则表达式对象。如果传入一个非正则表达式对象，则会隐式地使用 `new RegExp(obj)` 将其转换为一个 `RegExp` 。如果没有给出任何参数 ，将会得到一 个包含空字符串的 `Array` （即 `[""]` ）。

- 返回值：
  - 如果使用 g 标志，则将返回与完整正则表达式匹配的所有结果，但不会返回捕获组。
  - 如果未使用 g 标志，返回与 `RegExp.exec()` 相同的结果。仅返回第一个完整匹配及其相关的捕获组（`Array`）。 
  - 如果未找到匹配则为 `null`。



  ```js
var text = "cat, bat, sat, fat";
var pattern = /.at/;
var matches = text.match(pattern);	// 与 pattern.exec(text) 相同
alert(matches.index); 		// 0
alert(matches[0]);			 // "cat"
alert(pattern.lastIndex); 	// 0
  ```



#### **matchAll()**

**`matchAll()`** 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。

```
str.matchAll(regexp)
```

语法说明：

- 参数：正则表达式对象。如果所传参数不是一个正则表达式对象，则会隐式地使用 `new RegExp(obj)` 将其转换为一个 `RegExp` 。  `RegExp` 必须是设置了全局模式 `g` 的形式，否则会抛出异常 `TypeError`。

- 返回值：一个迭代器（不可重用，结果耗尽需要再次调用方法，获取一个新的迭代器）。



#### search()

> *str.search(regexp)*

search() 方法的参数与 match() 方法的参数相同：由字符串或 RegExp 对象指定的一个正则表达式。

search() 方法返回字符串中第一个匹配项的索引；如果没有找到匹配项，则返回 -1。

search() 方法不执行全局匹配，忽略标志 g ，并且始终是从字符串开头向后查找模式。

```js
var text = "abc, cat, bat, sat, fat";
var pos = text.search(/at/);
console.log(pos); 				// 6
```



#### replace()

**`replace()`** 方法返回一个由替换值（`replacement`）替换部分或所有的模式（`pattern`）匹配项后的新字符串。

```
str.replace(regexp|substr, newSubStr|function)
```

参数：

- 第一个参数（`pattern`）可以是一个 RegExp 对象或者一个字符串。
  - `regexp `：一个[`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/RegExp) 对象或者其字面量。该正则所匹配的内容会被第二个参数的返回值替换掉。
  - `substr `：一个将被 `newSubStr` 替换的字符串。其被视为一整个字符串，而不是一个正则表达式。仅第一个匹配项会被替换，要想替换所有子字符串，唯一的办法就是提供一个正则表达式，而且要指定全局（g）标志
- 第二个参数（`replacement`）可以是一个字符串或者一个函数。
  - `newSubStr`：用于替换掉第一个参数在原字符串中的匹配部分的字符串。该字符串中可以内插一些特殊的变量名。
  - `function` ：一个用来创建新子字符串的函数，该函数的返回值将替换掉第一个参数匹配到的结果。



```js
var text = "cat, bat, sat, fat";
var result = text.replace("at", "X");
console.log(result); 				// "cX, bat, sat, fat"
result = text.replace(/at/, "X");
console.log(result); 				// "cX, bat, sat, fat"
result = text.replace(/at/g, "X");
console.log(result); 				// "cX, bX, sX, fX"
```







#### split()

`split() ` 方法使用指定的分隔符字符串，将一个 `String` 对象分割成子字符串数组，以一个指定的分割字串来决定每个拆分的位置。 不改变原始字符串。

```js
str.split([separator[, limit]])
```

参数说明：

| 参数        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| *separator* | 可选。字符串或正则表达式，从该参数指定的地方分割 string Object。 |
| *limit*     | 可选。用于指定数组的大小。如果设置了该参数，以便确保返回的数组不会超过既定大小。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。 |

如果把空字符串 ("") 用作 separator，那么 stringObject 中的每个字符之间都会被分割。



### **localeCompare()**

localeCompare()，这个方法比较两个字符串，并返回下列值中的一个：

- 如果字符串在字母表中应该排在字符串参数之前，则返回一个负数（大多数情况下是-1，具体的值要视实现而定）；
- 如果字符串等于字符串参数，则返回0；
- 如果字符串在字母表中应该排在字符串参数之后，则返回一个正数（大多数情况下是1，具体的值同样要视实现而定）。

### fromCharCode()方法

### HTML 方法

以下方法并非标准方法，所以可能在某些浏览器下不支持。

| 方法                                                         | 描述                         |
| :----------------------------------------------------------- | :--------------------------- |
| [anchor()](https://www.runoob.com/jsref/jsref-anchor.html)   | 创建 HTML 锚。               |
| [big()](https://www.runoob.com/jsref/jsref-big.html)         | 用大号字体显示字符串。       |
| [blink()](https://www.runoob.com/jsref/jsref-blink.html)     | 显示闪动字符串。             |
| [bold()](https://www.runoob.com/jsref/jsref-bold.html)       | 使用粗体显示字符串。         |
| [fixed()](https://www.runoob.com/jsref/jsref-fixed.html)     | 以打字机文本显示字符串。     |
| [fontcolor()](https://www.runoob.com/jsref/jsref-fontcolor.html) | 使用指定的颜色来显示字符串。 |
| [fontsize()](https://www.runoob.com/jsref/jsref-fontsize.html) | 使用指定的尺寸来显示字符串。 |
| [italics()](https://www.runoob.com/jsref/jsref-italics.html) | 使用斜体显示字符串。         |
| [link()](https://www.runoob.com/jsref/jsref-link.html)       | 将字符串显示为链接。         |
| [small()](https://www.runoob.com/jsref/jsref-small.html)     | 使用小字号来显示字符串。     |
| [strike()](https://www.runoob.com/jsref/jsref-strike.html)   | 用于显示加删除线的字符串。   |
| [sub()](https://www.runoob.com/jsref/jsref-sub.html)         | 把字符串显示为下标。         |
| [sup()](https://www.runoob.com/jsref/jsref-sup.html)         | 把字符串显示为上标。         |



### 小结

String 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [charAt()](https://www.runoob.com/jsref/jsref-charat.html)   | 返回在指定位置的字符。                                       |
| [charCodeAt()](https://www.runoob.com/jsref/jsref-charcodeat.html) | 返回在指定的位置的字符的 Unicode 编码。                      |
| [concat()](https://www.runoob.com/jsref/jsref-concat-string.html) | 连接两个或更多字符串，并返回新的字符串。                     |
| [fromCharCode()](https://www.runoob.com/jsref/jsref-fromcharcode.html) | 将 Unicode 编码转为字符。                                    |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof.html) | 返回某个指定的字符串值在字符串中首次出现的位置。             |
| [includes()](https://www.runoob.com/jsref/jsref-string-includes.html) | 查找字符串中是否包含指定的子字符串。                         |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof.html) | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置。 |
| [match()](https://www.runoob.com/jsref/jsref-match.html)     | 查找找到一个或多个正则表达式的匹配。                         |
| [repeat()](https://www.runoob.com/jsref/jsref-repeat.html)   | 复制字符串指定次数，并将它们连接在一起返回。                 |
| [replace()](https://www.runoob.com/jsref/jsref-replace.html) | 在字符串中查找匹配的子串， 并替换与正则表达式匹配的子串。    |
| [search()](https://www.runoob.com/jsref/jsref-search.html)   | 查找与正则表达式相匹配的值。                                 |
| [slice()](https://www.runoob.com/jsref/jsref-slice-string.html) | 提取字符串的片断，并在新的字符串中返回被提取的部分。         |
| [split()](https://www.runoob.com/jsref/jsref-split.html)     | 把字符串分割为字符串数组。                                   |
| [startsWith()](https://www.runoob.com/jsref/jsref-startswith.html) | 查看字符串是否以指定的子字符串开头。                         |
| [substr()](https://www.runoob.com/jsref/jsref-substr.html)   | 从起始索引号提取字符串中指定数目的字符。                     |
| [substring()](https://www.runoob.com/jsref/jsref-substring.html) | 提取字符串中两个指定的索引号之间的字符。                     |
| [toLowerCase()](https://www.runoob.com/jsref/jsref-tolowercase.html) | 把字符串转换为小写。                                         |
| [toUpperCase()](https://www.runoob.com/jsref/jsref-touppercase.html) | 把字符串转换为大写。                                         |
| [trim()](https://www.runoob.com/jsref/jsref-trim.html)       | 去除字符串两边的空白                                         |
| [toLocaleLowerCase()](https://www.runoob.com/jsref/jsref-tolocalelowercase.html) | 根据本地主机的语言环境把字符串转换为小写。                   |
| [toLocaleUpperCase()](https://www.runoob.com/jsref/jsref-tolocaleuppercase.html) | 根据本地主机的语言环境把字符串转换为大写。                   |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-string.html) | 返回某个字符串对象的原始值。                                 |
| [toString()](https://www.runoob.com/jsref/jsref-tostring.html) | 返回一个字符串。                                             |















# 参考资料

- [JavaScript trim 实现（去除字符串首尾指定字符） - segmentfault](https://segmentfault.com/a/1190000002438098)
- [String.prototype.match() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)
- [String.prototype.matchAll() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)
- [String.prototype.replace() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)