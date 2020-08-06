#  Date

Date 类型提供了有关日期和时间的信息，包括当前日期和时间以及相关的计算功能。

ES 中的 Date 类型是在早期 Java 中的 java.util.Date 类基础上构建的。保存的日期能够精确到 1970 年 1 月 1 日之前或之后的 285 616 年。

## 创建对象

要创建一个日期对象，使用 new 操作符和 Date 构造函数即可。

`Date()` 构造函数有四种基本形式：

```js
var now = new Date();
new Date(value);
new Date(dateString);
new Date(year, monthIndex [, day [, hours [, minutes [, seconds [, milliseconds]]]]]);
```

- 没有参数：新创建的对象自动获得当前日期和时间。

- Unix 时间戳：根据特定的日期和时间创建日期对象，必须传入表示该日期的毫秒数（即从 UTC 时间 1970 年 1 月 1 日午夜起至该日期止经过的毫秒数）。忽略了闰秒。大多数 Unix 时间戳功能仅精确到最接近的秒。

- 时间戳字符串：表示日期的字符串值。该字符串应该能被 [`Date.parse()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/parse) 正确方法识别（即符合 [IETF-compliant RFC 2822 timestamps](http://tools.ietf.org/html/rfc2822#page-14) 或 [version of ISO8601](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15)）。

  由于浏览器差异和不一致性，强烈建议不要使用 `Date` 构造函数（和`Date.parse`，它们是等效的）解析日期字符串。

- 分别提供日期与时间的每一个成员

  - `year`：表示年份的整数值。 0到99会被映射至1900年至1999年，其它值代表实际年份。参见 [示例](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date#Two_digit_years_map_to_1900_-_1999)。

  - `monthIndex`：表示月份的整数值，从 0（1 月）到 11（12 月）。

  - `day` ：可选。表示一个月中的第几天的整数值，从 1 开始。默认值为 1。

  - `hours`：可选。表示一天中的小时数的整数值 (24 小时制)。默认值为 0（午夜）。

  - `minutes`：可选。表示一个完整时间（如 01:10:00）中的分钟部分的整数值。默认值为 0。

  - `seconds`：可选。表示一个完整时间（如 01:10:00）中的秒部分的整数值。默认值为 0。

  - `milliseconds`：可选。表示一个完整时间的毫秒部分的整数值。默认值为0。



## 属性

对象属性

- [`Date.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/prototype)：允许为 `Date` 对象添加属性。
- `Date.length`：值是 7。这是该构造函数可接受的参数个数。

所有的 `Date` 实例都继承自 `Date.prototype`。修改 `Date `构造函数的原型对象会影响到所有的 `Date` 实例。

实例属性

- `Date.prototype.constructor`：返回创建了实例的构造函数，默认是 [`Date`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Date) 构造函数。

实例方法

- Getter
- Setter
- Conversion getter



## 方法

### **Date.parse()**

> *Date*.parse(*datestring*)

Date.parse() 方法解析一个表示日期的字符串，返回 1970/1/1 午夜距离该日期时间的毫秒数。ECMA-262 没有定义参数的日期格式。通常有下列日期格式：

- 6/13/2004；
- January 12,2004；
- Tue May 25 2004 00:00:00 GMT-0700。
- ISO 8601 扩展格式 `YYYY-MM-DDTHH:mm:ss.sssZ`（例如2004-05-25T00:00:00）。只有兼容 ES 5 的实现支持这种格式。

```js
// 为 2004 年 5 月 25 日创建一个日期对象
var someDate = new Date(Date.parse("May 25, 2004"));
```

如果传入 Date.parse() 方法的字符串不能表示日期，那么它会返回 NaN。

如果直接将表示日期的字符串传递给 Date 构造函数，也会在后台调用 Date.parse()。下面的代码与前面的例子是等价的：

```js
var someDate = new Date("May 25, 2004");
```





### **Date.UTC()** 

> Date.UTC(*year*,*month*,*day*,*hours*,*minutes*,*seconds*,*millisec*)

Date.UTC() 方法返回指定的时间距 GMT 时间 1970 年 1 月 1 日午夜的毫秒数。

 UTC( Coordinated Universal Time ) ，国际协调时间，又称世界统一时间，世界标准时间。与 GMT(格林尼治时间)相同。

| 参数    | 描述                                 |
| :------ | :----------------------------------- |
| year    | 必需。表示年份的四位数字。           |
| month   | 必需。表示月份的整数，介于 0 ~ 11。  |
| day     | 必需。表示日期的整数，介于 1 ~ 31。  |
| hours   | 可选。表示小时的整数，介于 0 ~ 23。  |
| minutes | 可选。表示分钟的整数，介于 0 ~ 59。  |
| seconds | 可选。表示秒的整数，介于 0 ~ 59。    |
| ms      | 可选。表示毫秒的整数，介于 0 ~ 999。 |

例子：

```js
// GMT 时间2000 年1 月1 日午夜零时
var y2k = new Date(Date.UTC(2000, 0));
// GMT 时间2005 年5 月5 日下午5:55:55
var allFives = new Date(Date.UTC(2005, 4, 5, 17, 55, 55));
```

Date 构造函数也会模仿 Date.UTC()，接收的参数与 Date.UTC() 相同。但有一点明显不同：日期和时间都基于本地时区而非 GMT 来创建。

```js
// 本地时间2000 年1 月1 日午夜零时
var y2k = new Date(2000, 0);
// 本地时间2005 年5 月5 日下午5:55:55
var allFives = new Date(2005, 4, 5, 17, 55, 55);
```



### Data.now()

Data.now()方法，返回表示调用这个方法时的日期和时间的**毫秒数**。

```js
typeof Date.now();			// "number"
var start = Date.now();		// 取得开始时间
doSomething();				// 调用函数
var stop = Date.now();		// 取得停止时间
result = stop – start;
```

支持 Data.now() 方法的浏览器包括 IE9+、Firefox 3+、Safari 3+、Opera 10.5 和 Chrome。在不支持它的浏览器中，使用 + 操作符把 Data 对象转换成字符串，也可以达到同样的目的。

```js
var start = +new Date();	//取得开始时间
doSomething();			//调用函数
var stop = +new Date(),	//取得停止时间
result = stop - start;
```





### 继承的方法

与其他引用类型一样，Date 类型也重写了 toLocaleString()、toString() 和valueOf() 方法；但这些方法返回的值与其他类型中的方法不同。

- toLocaleString()：根据本地时间格式，把 Date 对象转换为字符串。
- toString()： 把 Date 对象转换为字符串。
- valueOf()：返回 Date 对象的原始值。



Date 类型的 valueOf() 方法，则根本不返回字符串，而是返回日期的毫秒表示。因此，可以方便使用比较操作符（小于或大于）来比较日期值。

```js
var date1 = new Date(2007, 0, 1); //"January 1, 2007"
var date2 = new Date(2007, 1, 1); //"February 1, 2007"
alert(date1 < date2); //true
alert(date1 > date2); //false
```





### 日期格式化方法

Date 类型还有一些专门用于将日期格式化为字符串的方法，这些方法如下。

- toDateString()——以特定于实现的格式显示星期几、月、日和年；
- toTimeString()——以特定于实现的格式显示时、分、秒和时区；
- toLocaleDateString()——以特定于地区的格式显示星期几、月、日和年；
- toLocaleTimeString()——以特定于实现的格式显示时、分、秒；
- toUTCString()——以特定于实现的格式完整的UTC 日期。

与 toLocaleString() 和 toString() 方法一样，以上这些字符串格式方法的输出也是因浏览器而异的，因此没有哪一个方法能够用来在用户界面中显示一致的日期信息。

> 除了前面介绍的方法之外，还有一个名叫 toGMTString() 的方法，这是一个与 toUTCString()等价的方法，其存在目的在于确保向后兼容。不过，ECMAScript 推荐现在编写的代码一律使用toUTCString()方法。





### 日期/时间组件方法

直接取得（get）和设置（set）日期值中特定部分的方法。

#### **getDate()**

getDate() 方法可返回月份的某一天。

```js
var d = new Date("July 21, 1983 01:15:00");
var n = d.getDate();			// 21
```

#### **setDate()** 

setDate() 方法用于设置一个月的某一天。

| 参数  | 描述                                                         |
| :---- | :----------------------------------------------------------- |
| *day* | 可选。表示月的某一天的数值，介于 1 ~ 31 之间（以本地时间计）。0 为上个月的最后一天；-1 为上个月的最后一天之前的一天。如果当月有 31 天：32 为下个月的第一天；如果当月有 30天：32 为下个月的第二天。 |

#### **setMonth()** 

setMonth() 方法用于设置月份。

> dateObj.setMonth(monthValue[, dayValue])

| 参数    | 描述                                                         |
| :------ | :----------------------------------------------------------- |
| *month* | 必需。表示月份的数值，介于 0 ~ 11之间。-1 为去年的最后一个月；12 为明年的第一个月；13 为明年的第二个月 |
| *day*   | 可选。表示月的某一天的数值，介于 1 ~ 31 之间（以本地时间计）。0 为上个月的最后一天；-1 为上个月的最后一天之前的一天。如果当月有 31 天：32 为下个月的第一天；如果当月有 30天：32 为下个月的第二天。 |





## 方法汇总

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **getDate()**                                                | 从 Date 对象返回一个月中的某一天 (1 ~ 31)。                  |
| [getDay()](https://www.runoob.com/jsref/jsref-getday.html)   | 从 Date 对象返回一周中的某一天 (0 ~ 6)。                     |
| [getFullYear()](https://www.runoob.com/jsref/jsref-getfullyear.html) | 从 Date 对象以四位数字返回年份。                             |
| [getHours()](https://www.runoob.com/jsref/jsref-gethours.html) | 返回 Date 对象的小时 (0 ~ 23)。                              |
| [getMilliseconds()](https://www.runoob.com/jsref/jsref-getmilliseconds.html) | 返回 Date 对象的毫秒(0 ~ 999)。                              |
| [getMinutes()](https://www.runoob.com/jsref/jsref-getminutes.html) | 返回 Date 对象的分钟 (0 ~ 59)。                              |
| [getMonth()](https://www.runoob.com/jsref/jsref-getmonth.html) | 从 Date 对象返回月份 (0 ~ 11)。                              |
| [getSeconds()](https://www.runoob.com/jsref/jsref-getseconds.html) | 返回 Date 对象的秒数 (0 ~ 59)。                              |
| [getTime()](https://www.runoob.com/jsref/jsref-gettime.html) | 返回 1970 年 1 月 1 日至今的毫秒数。                         |
| [getTimezoneOffset()](https://www.runoob.com/jsref/jsref-gettimezoneoffset.html) | 返回本地时间与格林威治标准时间 (GMT) 的分钟差。              |
| [getUTCDate()](https://www.runoob.com/jsref/jsref-getutcdate.html) | 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。              |
| [getUTCDay()](https://www.runoob.com/jsref/jsref-getutcday.html) | 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。               |
| [getUTCFullYear()](https://www.runoob.com/jsref/jsref-getutcfullyear.html) | 根据世界时从 Date 对象返回四位数的年份。                     |
| [getUTCHours()](https://www.runoob.com/jsref/jsref-getutchours.html) | 根据世界时返回 Date 对象的小时 (0 ~ 23)。                    |
| [getUTCMilliseconds()](https://www.runoob.com/jsref/jsref-getutcmilliseconds.html) | 根据世界时返回 Date 对象的毫秒(0 ~ 999)。                    |
| [getUTCMinutes()](https://www.runoob.com/jsref/jsref-getutcminutes.html) | 根据世界时返回 Date 对象的分钟 (0 ~ 59)。                    |
| [getUTCMonth()](https://www.runoob.com/jsref/jsref-getutcmonth.html) | 根据世界时从 Date 对象返回月份 (0 ~ 11)。                    |
| [getUTCSeconds()](https://www.runoob.com/jsref/jsref-getutcseconds.html) | 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。                    |
| getYear()                                                    | 已废弃。 请使用 getFullYear() 方法代替。                     |
| **parse()**                                                  | 返回1970年1月1日午夜到指定日期（字符串）的毫秒数。           |
| **setDate()**                                                | 设置 Date 对象中月的某一天 (1 ~ 31)。                        |
| [setFullYear()](https://www.runoob.com/jsref/jsref-setfullyear.html) | 设置 Date 对象中的年份（四位数字）。                         |
| [setHours()](https://www.runoob.com/jsref/jsref-sethours.html) | 设置 Date 对象中的小时 (0 ~ 23)。                            |
| [setMilliseconds()](https://www.runoob.com/jsref/jsref-setmilliseconds.html) | 设置 Date 对象中的毫秒 (0 ~ 999)。                           |
| [setMinutes()](https://www.runoob.com/jsref/jsref-setminutes.html) | 设置 Date 对象中的分钟 (0 ~ 59)。                            |
| **setMonth()**                                               | 设置 Date 对象中月份 (0 ~ 11)。                              |
| [setSeconds()](https://www.runoob.com/jsref/jsref-setseconds.html) | 设置 Date 对象中的秒钟 (0 ~ 59)。                            |
| [setTime()](https://www.runoob.com/jsref/jsref-settime.html) | setTime() 方法以毫秒设置 Date 对象。                         |
| [setUTCDate()](https://www.runoob.com/jsref/jsref-setutcdate.html) | 根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。              |
| [setUTCFullYear()](https://www.runoob.com/jsref/jsref-setutcfullyear.html) | 根据世界时设置 Date 对象中的年份（四位数字）。               |
| [setUTCHours()](https://www.runoob.com/jsref/jsref-setutchours.html) | 根据世界时设置 Date 对象中的小时 (0 ~ 23)。                  |
| [setUTCMilliseconds()](https://www.runoob.com/jsref/jsref-setutcmilliseconds.html) | 根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。                 |
| [setUTCMinutes()](https://www.runoob.com/jsref/jsref-setutcminutes.html) | 根据世界时设置 Date 对象中的分钟 (0 ~ 59)。                  |
| [setUTCMonth()](https://www.runoob.com/jsref/jsref-setutcmonth.html) | 根据世界时设置 Date 对象中的月份 (0 ~ 11)。                  |
| [setUTCSeconds()](https://www.runoob.com/jsref/jsref-setutcseconds.html) | setUTCSeconds() 方法用于根据世界时 (UTC) 设置指定时间的秒字段。 |
| setYear()                                                    | 已废弃。请使用 setFullYear() 方法代替。                      |
| [toDateString()](https://www.runoob.com/jsref/jsref-todatestring.html) | 把 Date 对象的日期部分转换为字符串。                         |
| toGMTString()                                                | 已废弃。请使用 toUTCString() 方法代替。                      |
| [toISOString()](https://www.runoob.com/jsref/jsref-toisostring.html) | 使用 ISO 标准返回字符串的日期格式。                          |
| [toJSON()](https://www.runoob.com/jsref/jsref-tojson.html)   | 以 JSON 数据格式返回日期字符串。                             |
| [toLocaleDateString()](https://www.runoob.com/jsref/jsref-tolocaledatestring.html) | 根据本地时间格式，把 Date 对象的日期部分转换为字符串。       |
| [toLocaleTimeString()](https://www.runoob.com/jsref/jsref-tolocaletimestring.html) | 根据本地时间格式，把 Date 对象的时间部分转换为字符串。       |
| [toLocaleString()](https://www.runoob.com/jsref/jsref-tolocalestring.html) | 根据本地时间格式，把 Date 对象转换为字符串。                 |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-date.html) | 把 Date 对象转换为字符串。                                   |
| [toTimeString()](https://www.runoob.com/jsref/jsref-totimestring.html) | 把 Date 对象的时间部分转换为字符串。                         |
| [toUTCString()](https://www.runoob.com/jsref/jsref-toutcstring.html) | 根据世界时，把 Date 对象转换为字符串。实例：`var today = new Date(); var UTCstring = today.toUTCString();` |
| **UTC()**                                                    | 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。        |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-date.html) | 返回 Date 对象的原始值。                                     |







# 参考资料

https://www.cnblogs.com/caoxueying2018/p/11202935.html