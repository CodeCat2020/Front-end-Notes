# 操作符

ECMA-262 描述了一组用于操作数据值的操作符符。



## **一元操作符**

只能操作一个值的操作符叫做一元操作符。

### 递增和递减

递增和递减操作符直接借鉴自 C，而且各有两个版本：前置型和后置型。

前置型变量的值都是在语句被求值以前改变的。（在计算机科学领域，这种情况通常被称作副效应。）

后置型变量的值都是在语句被求值之后改变的。

```js
var num1 = 2;
var num2 = 20;
console.log(
	--num1 + num2,		// 21
    num1 + num2,		// 21
    num1++ + num2,		// 21
    num1 + num2,		// 22
);
```

这 4 个操作符不仅适用于整数，还可以用于字符串、布尔值、浮点数值和对象。在应用于不同的值时，递增和递减操作符遵循下列规则。

- 应用于一个包含有效数字字符的字符串时，先将其转换为数字值，再执行加减 1 的操作。字符串变量变成数值变量。
- 应用于一个不包含有效数字字符的字符串时，将变量的值设置为 NaN。字符串变量变成数值变量。
- 应用于布尔值 false 时，先将其转换为 0 再执行加减 1 的操作。布尔值变量变成数值变量。
- 应用于布尔值 true 时，先将其转换为 1 再执行加减 1 的操作。布尔值变量变成数值变量。
- 应用于浮点数值时，执行加减 1 的操作。
- 应用于对象时，先调用对象的 valueOf() 方法以取得一个可供操作的值。然后对该值应用前述规则。如果结果是 NaN，则在调用 toString() 方法后再应用前述规则。对象变量变成数值变量。

```js
var s1 = "2", s2 = "2a", s3 = "z", b = false, f = 1.1;
var o = {
    valueOf: function() {
        return -1;
    }
};
s1++; s2++; s3++; b++; f--; o--;
console.log(s1, s2, s3, b, f, o);	// 3 NaN NaN 1 0.10000000000000009 -2
console.log(typeof s1);				// number
```



### 一元加和减

一元加操作符以一个加号（+）表示，放在数值前面，对数值不会产生任何影响。

一元减操作符主要用于表示负数。



## **算术操作符**

| 运算符 | 描述               |
| :----- | :----------------- |
| +      | 加法               |
| -      | 减法               |
| *      | 乘法               |
| /      | 除法               |
| %      | 系数，求模（余数） |
| ++     | 递加               |
| --     | 递减               |

### 加法（+） 

如果两个操作数都是数值，执行常规的加法计算，然后根据下列规则返回结果：

- 有一个操作数是 NaN，则结果是 NaN；
- 两个操作数都是 Infinity（或 -Infinity、+0、-0），则结果是 Infinity（或 -Infinity、+0、-0）；
- Infinity 加 -Infinity，则结果是 NaN；
- +0 加 -0，则结果是 +0。

如果有一个操作数是字符串，应用如下规则：

- 两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来；
- 只有一个操作数是字符串，则将另一个操作数转换为字符串，然后再将两个字符串拼接
  起来。

如果有一个操作数是对象、数值或布尔值，则调用它们的 toString() 方法取得相应的字符串值，然后再应用前面关于字符串的规则。对于undefined 和 null，则分别调用 String() 函数并取得字符串 "undefined" 和 "null"。

注意：加法操作符是左关联。

```js
var result2 = "2" + 3 + 4;	// "234"
var result2 = 3 + 2 + "7";	// "57"
```







### 减法（-）

减法在处理各种数据类型转换时，需要遵循一些特殊规则，如下所示：

- 如果两个操作符都是数值，则执行常规的算术减法操作并返回结果；
- 如果有一个操作数是 NaN，则结果是 NaN；
- 如果操作数都是 Infinity （或 -Infinity），则结果是 NaN；
- 如果是 Infinity 减 -Infinity，则结果是 Infinity；
- 如果是 -Infinity 减 Infinity，则结果是 -Infinity；
- 如果是 +0 减 +0，则结果是 +0；
- 如果是 +0 减 -0，则结果是 -0；
- 如果是 -0 减 -0，则结果是 +0；
- 如果有一个操作数是字符串、布尔值、null 或 undefined，则先在后台调用 Number() 函数将其转换为数值，然后再根据前面的规则执行减法计算。如果转换的结果是 NaN，则减法的结果就是 NaN；
- 如果有一个操作数是对象，则调用对象的 valueOf() 方法以取得表示该对象的数值。如果得到的值是 NaN，则减法的结果就是 NaN。





### 乘法（*）

在处理特殊值的情况下，乘法操作符遵循下列特殊的规则：

- 如果操作数都是数值，执行常规的乘法计算，即两个正数或两个负数相乘的结果还是正数。
  - 如果只有一个操作数有符号，那么结果是负数。
  - 如果乘积超过了 ECMAScript 数值的表示范围，则返回 Infinity 或 -Infinity；
- 如果有一个操作数是 NaN，则结果是 NaN；
- 如果是 Infinity 与 0 相乘，则结果是 NaN；
- 如果是 Infinity 与非 0 数值相乘，则结果是 Infinity 或 -Infinity，取决于有符号操作数的符号；
- 如果是 Infinity 与 Infinity 相乘，则结果是 Infinity；
- 如果有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的
  规则。





### 除法（/）

除法操作符对特殊的值也有特殊的处理规则。这些规则如下：

- 如果操作数都是数值，执行常规的除法计算，即两个正数或两个负数相除的结果还是正数。
  - 如果只有一个操作数有符号，那么结果就是负数。
  - 如果商超过了ECMAScript 数值的表示范围，则返回 Infinity 或 -Infinity；
- 如果有一个操作数是 NaN，则结果是 NaN；
-  Infinity 除以 Infinity ，结果是 NaN；
-  0 除以 0 ，结果是 NaN；
- 正数除以 0 返回 Infinity，负数除以 0 返回 -Infinity。
-  Infinity 除以非零数值，结果是 Infinity 或 -Infinity，取决于有符号操作数的符号；
- 如果有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的规则。

```js
console.log(
    (1/0),			// Infinity
    (-1/0),			// -Infinity
    (0/0),			// NaN
    isNaN(1/0),		// false
	isNaN(0/0),		//true
);
```



### 求模（%）

求模（余数）操作符由一个百分号（%）表示，遵循下列特殊规则来处理特殊的值：

- 操作数都是数值，执行常规的除法计算，返回除得的余数；
- 被除数是无穷大值，而除数是有限大的数值，则结果是 NaN；
- 被除数是有限大的数值，而除数是 0，则结果是 NaN；
-  Infinity 被 Infinity 除，则结果是 NaN；
- 被除数是有限大的数值，而除数是无穷大的数值，则结果是被除数；
- 被除数是 0，则结果是 0；
- 有一个操作数不是数值，则在后台调用 Number() 将其转换为数值，然后再应用上面的规则。





## **位操作符**

ECMAScript 中的所有数值都以 IEEE-754 64 位格式存储，但位操作符并不直接操作 64 位的值。而是先将 64 位的值转换成 32 位的整数，然后执行操作，最后再将结果转换回 64 位。对于开发人员来说，由于 64 位存储格式是透明的，因此整个过程就像是只存在 32 位的整数一样。

但这个转换过程也导致了一个严重的副效应，即在对特殊的 NaN 和 Infinity 值应用位操作时，这两个值都会被当成 0 来处理。

对于有符号的整数，32 位中的前 31 位用于表示整数的值。第 32 位用于表示数值的符号：0 表示正数，1 表示负数。这个表示符号的位叫做符号位，符号位的值决定了其他位数值的格式。

负数同样以二进制码存储，但使用的格式是二进制补码。

- 求这个数值绝对值的二进制码
- 求二进制反码
- 得到的二进制反码加 1。

如果对非数值应用位操作符，会先使用 Number() 函数将该值转换为一个数值（自动完成），然后再应用位操作。得到的结果将是一个数值。

| 运算符 | 描述         | 例子    | 等同于       | 结果 | 十进制 |
| :----- | :----------- | :------ | :----------- | :--- | :----- |
| &      | 与           | 5 & 1   | 0101 & 0001  | 0001 | 1      |
| \|     | 或           | 5 \| 1  | 0101 \| 0001 | 0101 | 5      |
| ~      | 非           | ~ 5     | ~0101        | 1010 | 10     |
| ^      | 异或         | 5 ^ 1   | 0101 ^ 0001  | 0100 | 4      |
| <<     | 零填充左位移 | 5 << 1  | 0101 << 1    | 1010 | 10     |
| >>     | 有符号右位移 | 5 >> 1  | 0101 >> 1    | 0010 | 2      |
| >>>    | 零填充右位移 | 5 >>> 1 | 0101 >>> 1   | 0010 | 2      |



```js
function func(a){
	a ^= (1 << 4) - 1;		// 等价于 a = a ^ [(1 << 4) - 1] 
	return a;
}
console.log(func(10));		// 5
```

运算过程：1 先化为二进制，然后左移 4 位，成 010000，再化为十进制得到 16，减 1 得到 15。 接着 a = 10，10 的二进制 => 1010，15 的二进制 => 1111，通过异或运算可以得到 0101，再转换成十进制即是 5。



## **布尔/逻辑操作符**



| 运算符 | 描述        |
| :----- | :---------- |
| &&     | 逻辑与，and |
| \|\|   | 逻辑或，or  |
| !      | 逻辑非，not |

### **逻辑非**（！）

逻辑非操作符首先会将它的操作数转换为一个布尔值，然后再对其求反，返回一个布尔值。

- 返回 false 的情况：操作数是对象、非空字符串、非零数值（包括 Infinity）。

- 返回 true 的情况：操作数是空字符串、数值 0 、null、NaN、underfined。


### **逻辑与（&&）**

逻辑与 `&&` 可以应用于任何类型的操作数，而不仅仅是布尔值。在有一个操作数不是布尔值的情况下，逻辑与操作不一定返回布尔值。此时，它遵循下列规则：

- 第一个操作数是对象，则返回第二个操作数；

- 第二个操作数是对象，则只有在第一个操作数的求值结果为 true 的情况下才会返回该对象；

- 两个操作数都是对象，则返回第二个操作数；

- 有一个操作数是 null（或 NaN、undefined），则返回 null（或 NaN、undefined）；

`&&` 属于短路操作，即如果第一个操作数的求值结果为 false，就不会再对第二个操作数求值。

```js
console.log(false && someUndefinedVariable); 	// false
console.log(true && someUndefinedVariable); 	// 报错 ReferenceError
```



### 逻辑或（||）

如果有一个操作数不是布尔值，逻辑或 `||` 也不一定返回布尔值。此时，它遵循下列规则：

- 第一个操作数是对象，则返回第一个操作数；

- 第一个操作数的求值结果为 false，则返回第二个操作数；

  ```js
  var a = 4399 < 0 || typeof(4399 + '');
  console.log(a);					// string
  ```

- 两个操作数都是对象，则返回第一个操作数；

- 两个操作数都是 null，则返回 null；

- 两个操作数都是 NaN，则返回 NaN；

- 两个操作数都是 undefined，则返回 undefined。

`||` 操作符也是短路操作符。如果第一个操作数的求值结果为 true，不会对第二个操作数求值。

```js
console.log(true || someUndefinedVariable); 	// true
console.log(false || someUndefinedVariable); 	// 报错 ReferenceError
```

利用逻辑或的这一行为来避免为变量赋 null 或 undefined 值。

如果 preferredObject 的值转换为 true，那么 myObject 的值为 preferredObject ；如果转换为 fasle，则 myObject 的值为 backupObject。

```js
var myObject = preferredObject || backupObject;
```





## **比较运算符**

| 运算符 | 描述                         |
| :----- | :--------------------------- |
| ==     | 等于                         |
| ===    | 严格等式运算符，**等值等型** |
| !=     | 不相等                       |
| !==    | 不等值或不等型               |
| >      | 大于                         |
| <      | 小于                         |
| >=     | 大于或等于                   |
| <=     | 小于或等于                   |
| ?      | 三元运算符                   |



### 关系操作符

小于（<）、大于（>）、小于等于（<=）和大于等于（>=）这几个关系操作符用于对两个值进行比较，都返回一个布尔值。

与 ECMAScript 中的其他操作符一样，当关系操作符的操作数使用了非数值时，也要进行数据转换或完成某些奇怪的操作。以下就是相应的规则。

- 两个操作数都是数值，则比较数值。

- 两个操作数都是字符串，则比较两个字符串对应的字符编码值。

  大写字母的字符编码全部小于小写字母的字符编码。如果要真正按字母表顺序比较字符串，就必须把两个操作数转换为相同的形式（全部大写或全部小写），然后再执行比较。

  ```js
  console.log(
      "Brick" < "alphabet",	// true, 字母 B 的字符编码为66，字母 a 对应 97。
      "Brick".toLowerCase() < "alphabet".toLowerCase() // false
  ); 
  ```

  比较两个数字字符串：

  ```js
  console.log("23" < "3"); // true，"2" 的字符编码是 50，而"3"的字符编码是 51。
  ```

- 一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较。

  ```js
  console.log("23" < 3); // false
  ```

- 

  ```js
  console.log(NaN < 3); // false
  console.log(NaN >= 3); // false
  ```

- 如果一个操作数是对象，则调用这个对象的 valueOf() 方法，用得到的结果按照前面的规则执行比较。如果对象没有 valueOf() 方法，则调用 toString() 方法，并用得到的结果根据前面的规则执行比较。

- 如果一个操作数是布尔值，则先将其转换为数值，然后再执行比较。



### 相等操作符

ECMAScript 提供两组操作符：相等和不相等——先转换再比较，全等和不全等——仅比较而不转换。

#### 相等和不相等

ECMAScript 中的相等操作符由两个等于号（==）表示，不相等操作符由叹号后跟等于号（!=）表示。这两个操作符都会先转换操作数（通常称为强制转型），然后再比较它们的相等性。

在转换不同的数据类型时，相等和不相等操作符遵循下列基本规则：

- 有一个操作数是布尔值，先将其转换为数值，再比较相等性；

  ```js
  console.log(true == 1,false == 0);    // true true
  ```

- 一个操作数是字符串，另一个操作数是数值，先将字符串转换为数值，再比较相等性；

  ```js
  console.log(
      "false" == 0,
      "false" == false,
      "5" == 5,
      "" == false,	
  );
  // false false true true
  ```

- 一个操作数是对象，另一个操作数不是，则调用对象的 valueOf() 方法，用得到的基本类型值按照前面的规则进行比较；

  ```js
  console.log(
      [] == true,		// false
      [] == false,	// true
      [] == 0,		// true
      [10] == 10		// true
      {} == true,		// false
      {} == false,	// false
      {} == 0,		// false
      {} == null,		// false
  );
  ```

  



这两个操作符在进行比较时则要遵循下列规则。

- null 和 undefined 是相等的。

  ```js
  console.log(null == undefined);	// true
  ```

- 要比较相等性之前，不能将 null 和 undefined 转换成其他任何值。

  ```js
  console.log(null == 0);			// false
  console.log(undefined == 0);	// false
  ```

- 如果有一个操作数是 NaN，则相等操作符返回 false，而不相等操作符返回 true。重要提示：
  即使两个操作数都是NaN，相等操作符也返回 false。

  ```js
  console.log(
      "NaN" == NaN,
      NaN == 3,
      NaN == NaN,
      NaN != NaN,
  );
  // false false false true
  ```

- 如果两个操作数都是对象，则比较它们是不是同一个对象。如果两个操作数都指向同一个对象，
  则相等操作符返回 true；否则，返回 false。









#### 全等和不全等

除了在比较之前不转换操作数之外，全等和不全等操作符与相等和不相等操作符没有什么区别。全
等操作符由 3 个等于号（===）表示，它只在两个操作数未经转换就相等的情况下返回 true。不全等操作符由一个叹号后跟两个等于号（!==）表示，它在两个操作数未经转换就不相等的情况下返回 true。

```js
console.log(null === undefined);	// false，它们是不同类型的值
console.log(NaN === NaN);		// false
```





- ==：等于。两边操作数类型不同时，先转换，再比较。
- ===：严格等于。仅比较而不转换。可以用来判断 null。
- Object.is()：加强版严格等于。与 === 基本一致，有两处不同：+0 不等于 -0；可以判断 NaN。

```js
console.log(null == undefined, null === undefined);		// true false
console.log(
    NaN == NaN,
    NaN === NaN,
	Object.is("str"/2, NaN),
);
// false false true
console.log(
    +0 == -0,
    +0 === -0,
    Object.is(+0, -0)
);
// true true false
```



## 条件操作符

> *variable = boolean_expression ? true_value : false_value;*

对 boolean_expression 求值（可能发生隐形类型转换），如果结果为 true，则给变量 variable 赋 true_value 值；如果求值结果为 false，则给变量 variable 赋 false_value 值。

```js
console.log(([]) ? true : false);	// true。解析：[] 隐式转换为 true。
```



## **赋值操作符**

如果在等于号（=）前面再添加乘性操作符、加性操作符或位操作符，就可以完成复合赋值操作。

设计这些操作符的主要目的就是简化赋值操作。使用它们不会带来任何性能的提升。

| 运算符 | 例子   | 等同于    |
| :----- | :----- | :-------- |
| =      | x = y  | x = y     |
| +=     | x += y | x = x + y |
| -=     | x -= y | x = x - y |
| *=     | x *= y | x = x * y |
| /=     | x /= y | x = x / y |
| %=     | x %= y | x = x % y |
| <<=    |        |           |
| >>=    |        |           |
| >>>=   |        |           |



## **逗号运算符**

使用逗号操作符可以在一条语句中执行多个操作。

逗号操作符多用于声明多个变量：

```js
var num1 = 1, num2 = 2, num3 = 3;
```

逗号操作符还可以用于赋值。在用于赋值时，逗号操作符总会返回表达式中的最后一项：

```js
var num = (5, 1, 4, 8, 0); 
console.log(num);			// 0
```





# 优先级、关联性

运算符的优先级决定了表达式中运算执行的先后顺序，优先级高的运算符最先被执行。

关联性决定了拥有相同优先级的运算符的执行顺序。考虑下面这个表达式：

```
a OP b OP c
```

左关联（左到右）相当于把左边的子表达式加上小括号 `(a OP b) OP c`，右关联（右到左）相当于 `a OP (b OP c)`。赋值运算符是右关联的。

下例中， `a` 和 `b` 的值都会成为 5。这是因为赋值运算符的返回结果就是赋值运算符右边的那个值，具体过程是：`b` 被赋值为5，然后 `a` 也被赋值为 `b=5` 的返回值，也就是 5。

```js
a = b = 5; 			// a = (b = 5)
console.log(a,b);	// 5 5 
```

示例：

```js
3 > 2 && 2 > 1
// return true

3 > 2 > 1
// 返回 false，因为 3 > 2 是 true，并且 true > 1 is false
// 加括号可以更清楚：(3 > 2) > 1
```



## **汇总表**

将所有运算符按照优先级的不同从高（20）到低（1）排列。

算术操作符 → 比较操作符 → 逻辑操作符 → "="赋值符号

如果同级的运算是按从左到右次序进行，多层括号由里向外。

| 优先级 | 运算类型                                                     | 关联性        | 运算符                                              |
| :----- | :----------------------------------------------------------- | :------------ | :-------------------------------------------------- |
| 20     | [`圆括号`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Grouping) | n/a（不相关） | `( … )`                                             |
| 19     | [`成员访问`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Property_Accessors#点符号表示法) | 从左到右      | `… . …`                                             |
|        | [`需计算的成员访问`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Property_Accessors#括号表示法) | 从左到右      | `… [ … ]`                                           |
|        | [`new`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new) (带参数列表) | n/a           | `new … ( … )`                                       |
|        | [函数调用](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Functions) | 从左到右      | `… ( … )`                                           |
|        | [可选链（Optional chaining）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Optional_chaining) | 从左到右      | `?.`                                                |
| 18     | [new](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/new) (无参数列表) | 从右到左      | `new …`                                             |
| 17     | [后置递增](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Increment)(运算符在后) | n/a           | `… ++`                                              |
|        | [后置递减](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Decrement)(运算符在后) | n/a           | `… --`                                              |
| 16     | [逻辑非](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_NOT)、[按位非](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_NOT) | 从右到左      | `! …` 、`~ …`                                       |
|        | [一元加法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Unary_plus)、[一元减法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Unary_negation) |               | `+ …` 、`- …`                                       |
|        | [前置递增](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Increment)、[前置递减](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Decrement) |               | `++ …` 、`-- …`                                     |
|        | [**typeof**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/typeof)、[void](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/void)、[delete](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/delete)、[await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await) |               | `typeof …`                                          |
| 15     | [幂](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Exponentiation) | 从右到左      | `… ** …`                                            |
| 14     | [乘法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Multiplication)、[除法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Division)、[取模](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Remainder) | 从左到右      | `… * …` 、`… / …` 、`… % …`                         |
| 13     | [加法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Addition)、[减法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Subtraction) | 从左到右      | `… + …` 、`… - …`                                   |
| 12     | [按位左移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)、[按位右移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)、[无符号右移](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) | 从左到右      | `… << …` 、`… >> …` 、`… >>> …`                     |
| 11     | [小于](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Less_than_operator)、[小于等于](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Less_than__or_equal_operator)、[大于](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Greater_than_operator)、[大于等于](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Greater_than_or_equal_operator) | 从左到右      | `… < …` 、`… <= …`                                  |
|        | [in](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/in)、[instanceof](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof) |               | `… in …` 、 `… instanceof …`                        |
| 10     | [**等号**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Equality)、[非等号](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Inequality)、[全等号](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Identity)、[非全等号](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Nonidentity) | 从左到右      | `… == …` 、`… != …` 、`… === …` 、`… !== …`         |
| 9      | [按位与](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_AND) | 从左到右      | `… & …`                                             |
| 8      | [按位异或](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_XOR) | 从左到右      | `… ^ …`                                             |
| 7      | [按位或](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_OR) | 从左到右      | `… | …`                                             |
| 6      | [逻辑与](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_AND) | 从左到右      | `… && …`                                            |
| 5      | [逻辑或](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_OR) | 从左到右      | `… || …`                                            |
| 4      | [条件运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) | 从右到左      | `… ? … : …`                                         |
| 3      | [**赋值**](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Assignment_Operators) | **从右到左**  | `… = …` 、`… += …` 、…… 、`… <<= …` 、…… 、`… &= …` |
| 2      | [yield](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/yield)、[yield*](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/yield*) | 从右到左      | `yield …` 、 `yield* …`                             |
| 1      | [展开运算符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_operator) | n/a           | `...` …                                             |
| 0      | [逗号](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Comma_Operator) | 从左到右      | `… , …`                                             |





# 参考资料

[运算符优先级 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

