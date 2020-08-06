




# JSON





## 简介



JSON（JavaScript Object Notation，JavaScript 对象表示法）是一个轻量级的**数据格式**，可以简化表示复杂数据结构的工作量。

JSON 是一种数据格式，不是一种编程语言。虽然具有相同的语法形式，但 JSON 并不从属于 JavaScript。

JSON 采用键值对的方式来组织数据，使用 JavaScript 语法的子集表示对象、数组、字符串、数值、布尔值和 null，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。 目前非常多的动态（PHP，JSP，.NET）编程语言都支持 JSON。





JSON 是存储和交换文本信息的语法，类似 XML。相比 XML，JSON 没有那么烦琐，而且在 JavaScript 中使用更便利。数据格式简单，易于读写， 占用更少的带宽。

- 在数据体量方面，相对于 XML 来讲， JSON 数据的体量小，传递的速度更快。
- 在数据交互方面， JSON 与 JavaScript 的交互更加方便，数据更容易解析，数据交互方式更灵活。
- 在数据描述方面， JSON 对数据的描述性比 XML 差。
- 在传输速度方面， JSON 传输的速度要远快于 XML 。




## 语法

JSON 的语法可以表示以下三种类型的值。

- 简单值：使用与 JavaScript 相同的语法，可以在 JSON 中表示字符串、数值、布尔值和 null。但 JSON 不支持 JavaScript 中的特殊值 undefined。
- 对象：一种复杂数据类型，表示一组无序的键值对儿。而每个键值对儿中的值可以是简单值，也可以是复杂数据类型的值。
- 数组：一种复杂数据类型，表示一组有序的值的列表，可以通过数值索引来访问其中的值。数组的值也可以是任意类型——简单值、对象或数组。

JSON 不支持变量、函数或对象实例，它就是一种表示结构化数据的格式，虽然与JavaScript 中表示数据的某些语法相同，但它并不局限于JavaScript 的范畴。

语法规则：

- 逗号分隔数据
- 大括号保存对象
- 方括号保存数组



### 简单值

最简单的 JSON 数据形式就是简单值。

下面是 JSON 表示字符串的方式：

```json
"Hello world!"
```

JavaScript 字符串与 JSON 字符串的最大区别在于，JSON 字符串必须使用双引号（单引号会导致语法错误）。





### 对象

JSON 表示上述对象的方式如下：

```json
{
    "name": "Nicholas",
    "age": 29
}
```

- 与 JavaScript 的对象字面量相比，JSON 对象没有声明变量，没有末尾的分号。
- JSON 对象的属性必须加双引号

属性的值可以是简单值，也可以是复杂类型值，因此可以像下面这样在对象中嵌入对象：

```JSON
{
    "name": "Nicholas",
    "age": 29,
    "school": {
        "name": "Merrimack College",
        "location": "North Andover, MA"
    }
}
```



### 数组

在 JSON 中，可以采用同样的语法表示同一个数组：

```
[25, "hi", true]
```

同样要注意，JSON 数组也没有变量和分号。把数组和对象结合起来，可以构成更复杂的数据集合。



## 解析与序列化



### JSON 对象



ECMAScript 5 对解析 JSON 的行为进行规范，定义了全局对象 JSON。原生的 JSON 对象得到了很多浏览器的支持，比如 IE8+、Firefox 3.5+、Safari 4+、Opera 10.5 和 Chrome。

JSON 对象有两个方法：stringify() 和 parse()。在最简单的情况下，这两个方法分别用于把 JavaScript 对象序列化为 JSON 字符串；把 JSON 字符串解析为原生JavaScript 值。

```js
var book = {							// JavaScript 对象
    title: "Professional JavaScript",
    authors: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
};
var jsonText = JSON.stringify(book);	// JSON 字符串
var bookCopy = JSON.parse(jsonText);	// 原生 JavaScript 值
```

在序列化 JavaScript 对象时，所有函数及原型成员都会被有意忽略，不体现在结果中。此外，值为 undefined 的任何属性也都会被跳过。结果中最终都是值为有效JSON 数据类型的实例属性。

默认情况下，JSON.stringify() 输出的 JSON 字符串不包含任何空格字符或缩进，因此保存在 `jsonText` 中的字符串如下所示：

```json
{"title":"Professional JavaScript","authors":["Nicholas C. Zakas"],"edition":3,"year":2011}
```

虽然 book 与 bookCopy 具有相同的属性，但它们是两个独立的、没有任何关系的对象。

这两个方法都有一些选项，通过它们可以改变过滤的方式，或者改变序列化的过程。



通过以下代码把 JSON 字符串转换为 JSON 对象。

```js
var obj1 = eval('(' + str + ')');
var obj3 = JSON.parse(str) ;
var obj3 = new Function('return (' + str + ')')()
```

通过以下代码把 JSON 对象转换为 JSON 字符串。

```js
var str2 = JSON.stringify(obj1) ;
```



### 序列化选项

```js
JSON.stringify(value[, replacer[, space]])
```

参数：

- value：必需， 要序列化的 JavaScript 值（通常为对象或数组）。

- replacer：可选，过滤器，可以是数组，也可以是函数。

  - 如果 replacer 是函数，传入的函数接收两个参数，属性（键）名和属性值。根据属性（键）名可以知道应该如何处理要序列化的对象中的属性。属性名只能是字符串，而在值并非键值对儿结构的值时，键名可以是空字符串。

    函数返回的值就是相应键的值。如果函数返回了 undefined，那么相应的属性会被忽略。根对象的键是一个空字符串：""。

  - 如果 replacer 是一个数组，则仅转换该数组中具有键值的成员（即数组中列出的属性）。成员的转换顺序与键在数组中的顺序一样。

- space：可选，一个选项，表示是否在 JSON 字符串中保留缩进。

  - 如果参数是一个数值，那它表示的是每个级别缩进的空格数。最大缩进空
    格数为 10，所有大于 10 的值都会自动转换为 10。
  - 如果缩进参数是一个字符串而非数值，则这个字符串将在 JSON 字符串中被用作缩进字符（不再使用空格）。在使用字符串的情况下，可以将缩进字符设置为制表符，或者两个短划线之类的任意字符。如：\t。



当过滤器是函数时，Firefox 3.5 和 3.6 会出现一个 bug：返回 undefined 意味着要跳过某个属性，而返回其他任何值都会在结果中包含相应的属性。Firefox 4 修复了这个bug。



**toJSON()方法**

假设把一个对象传入 JSON.stringify()，序列化该对象的顺序如下。

- (1) 如果存在toJSON()方法而且能通过它取得有效的值，则调用该方法。否则，返回对象本身。
- (2) 如果提供了第二个参数，应用这个函数过滤器。传入函数过滤器的值是第(1)步返回的值。
- (3) 对第(2)步返回的每个值进行相应的序列化。
- (4) 如果提供了第三个参数，执行相应的格式化。

无论是考虑定义 toJSON() 方法，还是考虑使用函数过滤器，亦或需要同时使用两者，理解这个顺序都是至关重要的。



### 解析选项

```
JSON.parse(text[, reviver])
```

**参数说明：**

- *text*：必需， 一个有效的 JSON 字符串。如果字符串不是有效的 JSON，该方法会抛出错误。
- *reviver*：可选，还原函数，将为对象的每个成员调用此函数。接收两个参数，一个键和一个值，而且都需要返回一个值。
  - 如果还原函数返回 undefined，则表示要从结果中删除相应的键；
  - 如果返回其他值，则将该值插入到结果中。



早期的 JSON 解析器基本上就是使用 JavaScript 的 eval() 函数。由于 JSON 是 JavaScript 语法的子集，因此 eval() 函数可以解析、解释并返回 JavaScript 对象和数组。



推荐使用 JSON.parse()，eval会执行json数据中的恶意代码







# JWT







# 参考资料

- [JavaScript JSON - 菜鸟教程](https://www.runoob.com/js/js-json.html)
- [JSON - MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
- [JSONLint](https://jsonlint.com/)













