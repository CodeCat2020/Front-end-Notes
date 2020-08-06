# RegExp 类型

**`RegExp`** 对象用于将文本与一个模式匹配。

RegExp 类型是 ECMAScript 支持正则表达式的一个接口，提供了最基本的和一些高级的正则表达式功能。

## 创建对象

有两种方法可以创建一个 `RegExp` 对象：一种是字面量，另一种是构造函数。

- 字面量：由斜杠包围而不是引号包围。当正则表达式保持为常量时，使用字面量。语法：

  ```js
  // 类似 Perl 的语法，创建一个正则表达式
  var expression = / pattern / flags ; 
  ```

  当表达式被赋值时，字面量形式提供正则表达式的编译（compilation）状态，在循环中使用字面量构造一个正则表达式时，正则表达式不会在每一次迭代中都被重新编译（recompiled）。

- 构造函数的字符串参数：由引号而不是斜杠包围。

  以下三种表达式都会创建相同的正则表达式：

  ```js
  /ab+c/i;
  new RegExp('ab+c', 'i');
  new RegExp(/ab+c/, 'i');
  ```

  正则表达式对象的构造函数，提供了正则表达式运行时编译（runtime compilation）。如果知道正则表达式模式将会改变，或者事先不知道什么模式，而是从另一个来源获取（比如用户输入），这些情况都可以使用构造函数。



### 构造函数中的标志参数(flags)

每个正则表达式都可带有一或多个标志（flags），用以标明正则表达式的行为。正则表达式的匹配模式支持下列 3 个标志。

- g：表示全局（global）模式，是否全文搜索，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
- i：表示<u>不区分大小写</u>（case-insensitive）模式，是否大小写敏感，即在确定匹配项时忽略模式与字符串的大小写；
- m：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

```js
/* 匹配字符串中所有"at"的实例*/
var pattern1 = /at/g;
/* 匹配第一个"bat"或"cat"，不区分大小写*/
var pattern2 = /[bc]at/i;
/* 匹配所有以"at"结尾的 3 个字符的组合，不区分大小写*/
var pattern3 = /.at/gi;
```



当使用构造函数创造正则对象时，需要常规的字符转义规则（在前面加反斜杠 `\`）。

```js
var re = new RegExp("\\w+");
var re = /\w+/;					// 与上面的正则表达式等价
```

### 元字符

正则表达式由两种基本字符类型组成：原义文本字符和元字符。元字符是在正则表达式中有特殊含义的非字母字符。

与其他语言中的正则表达式类似，模式中使用的所有元字符都必须转义（在字符前面加反斜杠 `\`）。正则表达式中的元字符包括： `( [ { \ ^ $ | ) ? * + .]}`

```js
/* 匹配所有以"at"结尾的 3 个字符的组合，不区分大小写*/
var pattern3 = /.at/gi;
/* 匹配所有".at"，不区分大小写*/
var pattern4 = /\.at/gi;
```



## 实例属性

RegExp 的每个实例都具有下列属性，通过这些属性可以取得有关模式的各种信息。

- [`RegExp.prototype.flags`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/flags)：含有 `RegExp` 对象 flags 的字符串。
- [`RegExp.prototype.dotAll`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/dotAll)：`.` 是否要匹配新行（newlines）。
- global：布尔值，默认是 false，表示是否设置了 g 标志。
- ignoreCase：布尔值，默认是 false，表示是否设置了 i 标志。匹配文本时是否忽略大小写。
- lastIndex：整数，表示开始搜索下一个匹配项的字符位置（当前表达式匹配内容的最后一个字符的下一个位置），从 0 算起。
- multiline：布尔值，默认是 false，表示是否设置了 m 标志。是否进行多行搜索。
- source：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。
- [`RegExp.prototype.sticky`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/sticky)：搜索是否是 sticky。
- [`RegExp.prototype.unicode`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/unicode)：Unicode 功能是否开启。

```js
var pattern1 = /\[bc\]at/i;
console.log(
    pattern1.global,		 		// false
    pattern1.ignoreCase,			// true
    pattern1.multiline,				// false
    pattern1.lastIndex,				// 0
    pattern1.source,				// "\[bc\]at"
);	
var pattern2 = new RegExp("\\[bc\\]at", "gim");
console.log(
    pattern2.global,		 		// true
    pattern2.ignoreCase,			// true
    pattern2.multiline,				// true
    pattern2.lastIndex,				// 0
    pattern2.source,				// "\[bc\]at"
);
```







## 实例方法

哪个不是 RegExp 对象的方法？

| 方法                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| [compile](https://www.runoob.com/jsref/jsref-regexp-compile.html) | 在 1.5 版本中已废弃。 编译正则表达式。             |
| [exec](https://www.runoob.com/jsref/jsref-exec-regexp.html)  | 检索字符串中指定的值。返回找到的值，并确定其位置。 |
| [test](https://www.runoob.com/jsref/jsref-test-regexp.html)  | 检索字符串中指定的值。返回 true 或 false。         |
| [toString](https://www.runoob.com/jsref/jsref-regexp-tostring.html) | 返回正则表达式的字符串。                           |



### exec()

exec() 方法是专门为捕获组而设计的，用于检索字符串中的正则表达式的匹配。

```
regexObj.exec(str)
```

语法说明：

- 参数：要匹配正则表达式的字符串。

- 匹配成功，<u>返回包含第一个匹配项信息的数组</u>，并更新正则表达式对象的 `lastIndex` 属性。返回的数组是 Array 的实例，但包含额外的属性：

  - `index` ：表示匹配项在字符串中的位置；
  - `input` ：表示应用正则表达式的字符串。
  - `groups`： 一个捕获组数组 或 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)（如果没有定义命名捕获组）。

  完全匹配成功的文本将作为返回数组的第一项，从第二项起，后续每项都对应正则表达式内捕获括号里匹配成功的文本。

- 匹配失败，返回 `null`，并将 [`lastIndex`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/lastIndex) 重置为 0 。

**非全局模式 vs 全局模式**

对于 exec() 方法而言，即使在模式中设置了全局标志（g），它每次也只会返回一个匹配项。

- 在不设置全局标志的情况下，在同一个字符串上多次调用 exec() 将始终返回第一个匹配项的信息。`lastIndex` 属性不会改变。
- 而在设置全局标志的情况下，每次调用 exec() 则都会在字符串中继续查找新匹配项。`lastIndex` 属性会改变。

```js
var text = "abc cat, bat, sat, fat";
var pattern1 = /.at/;
var pattern2 = /.at/g;

var matches = pattern1.exec(text);
console.log(matches.length,matches.index,matches[0],pattern1.lastIndex);  
// 输出 1 4 cat 0

matches = pattern1.exec(text);
console.log(matches.length,matches.index,matches[0],pattern1.lastIndex); 
// 输出 1 4 cat 0

var matches = pattern2.exec(text);
console.log(matches.length,matches.index,matches[0],pattern2.lastIndex); 
// 输出 1 4 cat 7

matches = pattern2.exec(text);
console.log(matches.length,matches.index,matches[0],pattern2.lastIndex); 
// 输出 1 9 cat 12
```

**分组**

```js
var text = "The Quick Brown Fox Jumps Over The Lazy Dog";
var pattern = /quick\s(brown).+?(jumps)/ig;
var matches = pattern.exec(text);

console.log(
    matches.length,		// 3
    matches.index,		// 4
    matches[0],			// Quick Brown Fox Jumps
    pattern.lastIndex	// 25
); 
console.log(matches[1]); 	// Brown
console.log(matches[2]); 	// Jumps
```



### **test()**

test() 方法用于检测一个字符串是否匹配某个模式，<u>返回的是布尔值</u>。如果字符串中有匹配的值返回 true ，否则返回 false。

```
regexObj.test(str)
```

在只想知道目标字符串与某个模式是否匹配，但不需要知道其文本内容的情况下，使用这个方法非常方便。因此，test() 方法经常被用在 if 语句中。

```js
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;
if (pattern.test(text)){
    alert("The pattern was matched.");
}
```

如果正则表达式设置了全局标志，`test() ` 的执行会改变正则表达式 `lastIndex` 属性。连续的执行 `test()` 方法，后续的执行将会从 lastIndex 处开始匹配字符串。（`exec()` 同样改变正则本身的 `lastIndex`属性值）。

```js
var reg1 = /\w/;
var reg2 = /\w/g;
while(reg2.test('ab')){
	console.log(reg2.lastIndex);		// 1 2
}
console.log(reg2.test('a'));		// true
console.log(reg2.test('a'));		// false
console.log(reg2.test('a'));		// true
```



### toString() 

RegExp 实例继承的 toLocaleString() 和 toString() 方法都会返回正则表达式的字面量，与创建正则表达式的方式无关。







## 构造函数属性

| 长属性名     | 短属性名 | 说明                                                         |
| ------------ | -------- | ------------------------------------------------------------ |
| input        | $_       | 最近一次要匹配的字符串。Opera未实现此属性                    |
| lastMatch    | $&       | 最近一次的匹配项。Opera未实现此属性                          |
| lastParen    | $+       | 最近一次匹配的捕获组。Opera未实现此属性                      |
| leftContext  | $`       | input字符串中lastMatch之前的文本                             |
| multiline    | $*       | 布尔值，表示是否所有表达式都使用多行模式。IE和Opera未实现此属性 |
| rightContext | $'       | Input字符串中lastMatch之后的文本                             |





## 模式的局限性

ECMAScript 正则表达式不支持的特性：

- 匹配字符串开始和结尾的\A 和\Z 锚，但支持以插入符号（^）和美元符号（$）来匹配字符串的开始和结尾。
- 向后查找（lookbehind），但完全支持向前查找（lookahead）。
- 并集和交集类
- 原子组（atomic grouping）
- Unicode 支持（单个字符除外，如\uFFFF）
- 命名的捕获组，但支持编号的捕获组。
- s（single，单行）和 x（free-spacing，无间隔）匹配模式
- 条件匹配
- 正则表达式注释







# 参考资料

- [JavaScript 正则表达式 - 慕课网课程](https://www.imooc.com/learn/706)
- [JavaScript 正则表达式 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)
- [JavaScript 正则表达式 - 菜鸟教程](https://www.runoob.com/js/js-regexp.html)







