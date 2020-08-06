

# 单体内置对象

在所有代码执行之前，作用域中就已经存在两个内置对象：Global 和 Math。

在大多数ECMAScript 实现中都不能直接访问 Global 对象；不过，Web 浏览器实现了承担该角色的 window 对象。全局变量和函数都是 Global 对象的属性。

Math 对象提供了很多属性和方法，用于辅助完成复杂的数学计算任务。

## Global 对象

事实上，没有全局变量或全局函数；所有在全局作用域中定义的属性和函数，都是 Global 对象的属性。

### 全局属性

ECMAScript 5 明确禁止给 undefined、NaN 和 Infinity 赋值，这样做即使在非严格模式下也会导致错误。

| 属性                                                         | 描述                     |
| :----------------------------------------------------------- | :----------------------- |
| [Infinity](https://www.runoob.com/jsref/jsref-infinity.html) | 代表正的无穷大的数值。   |
| [NaN](https://www.runoob.com/jsref/jsref-nan.html)           | 指示某个值是不是数字值。 |
| [undefined](https://www.runoob.com/jsref/jsref-undefined.html) | 指示未定义的值。         |

### 全局函数

| 函数                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [decodeURI()](https://www.runoob.com/jsref/jsref-decodeuri.html) | 解码某个编码的 URI。                                         |
| [decodeURIComponent()](https://www.runoob.com/jsref/jsref-decodeuricomponent.html) | 解码一个编码的 URI 组件。                                    |
| [encodeURI()](https://www.runoob.com/jsref/jsref-encodeuri.html) | 把字符串编码为 URI。                                         |
| [encodeURIComponent()](https://www.runoob.com/jsref/jsref-encodeuricomponent.html) | 把字符串编码为 URI 组件。                                    |
| [**escape**()](https://www.runoob.com/jsref/jsref-escape.html) | 对字符串进行编码。                                           |
| [**eval**()](https://www.runoob.com/jsref/jsref-eval.html)   | 计算 JavaScript 字符串，并把它作为脚本代码来执行。返回字符串表达式中的值。 |
| [isFinite()](https://www.runoob.com/jsref/jsref-isfinite.html) | 检查某个值是否为有穷大的数。                                 |
| [isNaN()](https://www.runoob.com/jsref/jsref-isnan.html)     | 检查某个值是否是数字。                                       |
| [Number()](https://www.runoob.com/jsref/jsref-number.html)   | 把对象的值转换为数字。                                       |
| [**parseFloat**()](https://www.runoob.com/jsref/jsref-parsefloat.html) | 解析一个字符串并返回一个浮点数。                             |
| [parseInt()](https://www.runoob.com/jsref/jsref-parseint.html) | 解析一个字符串并返回一个整数。                               |
| [String()](https://www.runoob.com/jsref/jsref-string.html)   | 把对象的值转换为字符串。                                     |
| [unescape()](https://www.runoob.com/jsref/jsref-unescape.html) | 对由 escape() 编码的字符串进行解码。返回字符串ASCII 码       |



### URI 编码方法

#### **encodeURI() 和 encodeURIComponent()** 

这两个方法可以对 URI 进行编码。它们用特殊的 UTF-8 编码替换所有无效的字符，从而让浏览器能够接受和理解。

```js
encodeURI(URI));
encodeURIComponent(str);	// URI 的组成部分。
```

- encodeURI() 主要用于整个 URI，而 encodeURIComponent() 主要用于对 URI 中的某一段进行编码。

- 它们的主要区别在于：encodeURI() 不会对本身属于 URI 的特殊字符进行编码，例如冒号、正斜杠、问号和井字号；而 encodeURIComponent() 则会对它发现的任何非标准字符进行编码。





#### **decodeURI() 和 decodeURIComponent()**

decodeURI() 只能对使用 encodeURI() 替换的字符进行解码。例如，它可将 %20 替换成一个空格，但不会对 %23（#） 作任何处理，而井字号不是使用 encodeURI() 替换的。

同样地，decodeURIComponent() 能够解码使用 encodeURIComponent() 编码的所有字符，即它可以解码任何特殊字符的编码。







### **eval() **

> eval(string)

`eval()` 函数会将传入的字符串当做 JavaScript 代码进行执行。

```js
eval("alert('hi')");	// 等价于 alert("hi");
```

当解析器发现代码中调用 eval() 方法时，它会将传入的参数当作实际的 ECMAScript 语句来解析，然后把执行结果插入到原位置。通过 eval() 执行的代码被认为是包含该次调用的执行环境的一部分，因此被执行的代码具有与该执行环境相同的作用域链。这意味着通过 eval() 执行的代码可以引用在包含环境中定义的变量。

`eval()` 可以延长作用域链。下例中，变量 msg 是在 eval() 调用的环境之外定义的，但其中调用的 alert() 仍然能够显示"hello world"。这是因为第二行代码最终被替换成了一行真正的代码。

```js
var msg = "hello world";
eval("alert(msg)"); //"hello world"
```

在 eval() 中创建的任何变量或函数都不会被提升，因为在解析代码的时候，它们被包含在一个字符串中；它们只在 eval() 执行的时候创建。

严格模式下，在外部访问不到 eval() 中创建的任何变量或函数。



应该避免使用 eval ，它会造成程序不安全，非常影响性能（执行两次， 一次解析成 JavaScript 语句， 一次执行）。

能够解释代码字符串的能力非常强大，但也非常危险。因此在使用 eval() 时必须极为谨慎，特别是在用它执行用户输入数据的情况下。否则，可能会有恶意用户输入威胁你的站点或应用程序安全的代码（即所谓的代码注入）。





## Math对象

Math 对象用于执行数学任务，是一个内置对象，它拥有一些数学常数属性和数学函数方法。

`Math` 用于 [`Number`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number) 类型。它不支持 [`BigInt`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/BigInt)。

与其他全局对象不同的是，`Math` 不是一个构造器。`Math` 的所有属性与方法都是静态的。

### 属性

`Math` 的常量是使用 JavaScript 中的全精度浮点数来定义的。

| 属性                                                       | 描述                                                    |
| :--------------------------------------------------------- | :------------------------------------------------------ |
| [E](https://www.runoob.com/jsref/jsref-e.html)             | 返回算术常量 e，即自然对数的底数（约等于2.718）。       |
| [LN2](https://www.runoob.com/jsref/jsref-ln2.html)         | 返回 2 的自然对数（约等于0.693）。                      |
| [LN10](https://www.runoob.com/jsref/jsref-ln10.html)       | 返回 10 的自然对数（约等于2.302）。                     |
| [LOG2E](https://www.runoob.com/jsref/jsref-log2e.html)     | 返回以 2 为底的 e 的对数（约等于 1.4426950408889634）。 |
| [LOG10E](https://www.runoob.com/jsref/jsref-log10e.html)   | 返回以 10 为底的 e 的对数（约等于0.434）。              |
| [PI](https://www.runoob.com/jsref/jsref-pi.html)           | 返回圆周率（约等于3.14159）。                           |
| [SQRT1_2](https://www.runoob.com/jsref/jsref-sqrt1-2.html) | 返回 2 的平方根的倒数（约等于 0.707）。                 |
| [SQRT2](https://www.runoob.com/jsref/jsref-sqrt2.html)     | 返回 2 的平方根（约等于 1.414）。                       |



### 方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [abs(x)](https://www.runoob.com/jsref/jsref-abs.html)        | 返回 x 的绝对值。                                            |
| [acos(x)](https://www.runoob.com/jsref/jsref-acos.html)      | 返回 x 的反余弦值。                                          |
| [asin(x)](https://www.runoob.com/jsref/jsref-asin.html)      | 返回 x 的反正弦值。                                          |
| [atan(x)](https://www.runoob.com/jsref/jsref-atan.html)      | 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。     |
| [atan2(y,x)](https://www.runoob.com/jsref/jsref-atan2.html)  | 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。 |
| [ceil(x)](https://www.runoob.com/jsref/jsref-ceil.html)      | 对数进行上舍入。                                             |
| [cos(x)](https://www.runoob.com/jsref/jsref-cos.html)        | 返回数的余弦。                                               |
| [exp(x)](https://www.runoob.com/jsref/jsref-exp.html)        | 返回 Ex 的指数。                                             |
| [floor(x)](https://www.runoob.com/jsref/jsref-floor.html)    | 对 x 进行下舍入。                                            |
| [log(x)](https://www.runoob.com/jsref/jsref-log.html)        | 返回数的自然对数（底为e）。                                  |
| [max(x,y,z,...,n)](https://www.runoob.com/jsref/jsref-max.html) | 返回 x,y,z,...,n 中的最高值。                                |
| [min(x,y,z,...,n)](https://www.runoob.com/jsref/jsref-min.html) | 返回 x,y,z,...,n中的最低值。                                 |
| [pow(x,y)](https://www.runoob.com/jsref/jsref-pow.html)      | 返回 x 的 y 次幂。                                           |
| [random()](https://www.runoob.com/jsref/jsref-random.html)   | 返回 0 ~ 1 之间的随机数。                                    |
| [round(x)](https://www.runoob.com/jsref/jsref-round.html)    | 四舍五入。                                                   |
| [sin(x)](https://www.runoob.com/jsref/jsref-sin.html)        | 返回数的正弦。                                               |
| [sqrt(x)](https://www.runoob.com/jsref/jsref-sqrt.html)      | 返回数的平方根。                                             |
| [tan(x)](https://www.runoob.com/jsref/jsref-tan.html)        | 返回角的正切。                                               |



#### ceil()

ceil() 方法可对一个数进行向上取整。返回大于或等于函数参数，并且与之最接近的整数。

#### floor()

floor() 方法可对一个数进行向下取整。返回小于或等于函数参数，并且与之最接近的整数。





#### max()

> *Math.max(value1[,value2, ...])* 

`Math.max()` 函数返回一组数中的最大值。如果给定的参数中至少有一个参数无法被转换成数字，则会返回 [`NaN`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)。





#### random()

> *Math.random()*

返回介于 0（包含） ~ 1（不包含） 之间的一个随机数。



生成指定范围内的随机数

```js
function setRadomNum(min,max){
    return  Math.floor(Math.random() * (max - min + 1)) + min;
}
```



#### round()

> *Math.round(x)*

round() 方法可把一个数字**四舍五入为最接近的整数**。

如果 x 与两侧整数同等接近，则结果接近 +∞ 方向的数字值 。

```js
var a = Math.round(2.60);		// 3
var b = Math.round(2.50);		// 3
var c = Math.round(2.49);		// 2
var d = Math.round(-2.60);	// -3
var e = Math.round(-2.50);	// -2
var f = Math.round(-2.49);	// -2，距离-2为0.49，距离-3为0.51
var g = Math.round(-2.51);	// -3，距离-2为0.51，距离-3为0.49
```








