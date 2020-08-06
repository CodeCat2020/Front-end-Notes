# 简介

ECMAScript 是 JavaScript 的规格，JavaScript 是 ECMAScript 的一种实现。



ECMAScript 版本

| 年份 | 名称           | 描述                                              |
| :--- | :------------- | :------------------------------------------------ |
| 1997 | ECMAScript 1   | 第一个版本                                        |
| 1998 | ECMAScript 2   | 版本变更                                          |
| 1999 | ECMAScript 3   | 添加正则表达式 添加 try/catch                     |
| 2000 | ECMAScript 4   | 没有发布。太激进，分歧太大。ES6 制定的起点。      |
| 2009 | ECMAScript 5   | 添加 "strict mode"，严格模式 添加 JSON 支持       |
| 2011 | ECMAScript 5.1 | 版本变更                                          |
| 2015 | ECMAScript 6   | 添加类和模块                                      |
| 2016 | ECMAScript 7   | 增加指数运算符 (**) 增加 Array.prototype.includes |
| 2017 | ECMAScript 8   |                                                   |
| 2018 | ECMAScript 9   |                                                   |
| 2019 | ECMAScript 10  |                                                   |
| 2020 | ECMAScript 11  |                                                   |



**ES6 与 ECMAScript 2015 的关系**

ES6 一般指 ES2015 标准，但有时也泛指“下一代 JavaScript 语言”，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等。

ECMAScript 2015（简称 ES2015） 是正式名称，特指该年发布的正式版本的语言标准。





**Babel 转码器**

[Babel](https://babeljs.io/) 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。

```js
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```

上面代码中，原始代码用了箭头函数，Babel 将其转为普通函数，就能在不支持箭头函数的 JavaScript 环境执行了。



# 新特性



## ECMAScript 2015





## ECMAScript  2016



- Array.prototype.includes ：如果参数value 在当前数组中，返回true ；否则，返回false 。
  下面结合一个简单的例子来使用includes 方法。

  ```js
  var array = [l , 2 , 3];
  var result = array.includes(l) ;
  ```

  此时 result 的值为 true 。注意， includes() 能够在数组中寻找NaN

- 取幂运算符：“＊＊”表示的是取幂运算。





## ECMAScript 2017

async、await





## ECMAScript 2018





## ECMAScript 2019



## ECMAScript 2020





