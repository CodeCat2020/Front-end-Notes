# 引用类型

在 ECMAScript 中，引用类型是一种数据结构，将数据和功能组织在一起。对象被称为引用类型的值，是某个特定引用类型的实例。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

引用类型与类相似，但实现不同。ECMAScript 面向对象，但它不具备传统的面向对象语言所支持的类和接口等基本结构。

## 内置对象



ECMAScript 提供了一些内置的引用类型用来创建特定的对象。

- Object 是一个基础类型，其他所有类型都从 Object 继承基本的行为；
- Array 类型是一组值的有序列表，同时还提供了操作和转换这些值的功能；
- Date 类型提供了有关日期和时间的信息，包括当前日期和时间以及相关的计算功能；
- RegExp 类型是 ECMAScript 支持正则表达式的一个接口，提供了最基本的和一些高级的正则表达式功能。
- 函数是 Function 类型的实例，因此函数也是对象；这一点正是 JavaScript 最有特色的地方。由于函数是对象，所以函数也拥有方法，可以用来增强其行为。

- 通过基本包装类型，JavaScript 中的基本类型值可以被当作对象来访问。三种基本包装类型分别是：Boolean、Number 和 String。以下是它们共同的特征：
  - 每个包装类型都映射到同名的基本类型；
  - 在读取模式下访问基本类型值时，就会创建对应的基本包装类型的一个对象，从而方便了数据操作；
  - 操作基本类型值的语句一经执行完毕，就会立即销毁新创建的包装对象。
- 在所有代码执行之前，作用域中已经存在两个内置对象：Global 和 Math。
  - 在大多数 ECMAScript 实现中都不能直接访问 Global 对象；不过，Web 浏览器实现了承担该角色的 window 对象。全局变量和函数都是 Global 对象的属性。
  - Math 对象提供了很多属性和方法，用于辅助完成复杂的数学计算任务。







## **创建对象**



创建对象有 4 种方式。

- 使用 new 操作符和对象构造函数， `var obj = new Object()`  。
- 使用对象字面量， `var obj = {}` 。（最常用）
- 使用类的实例化方式， `var obj = new Person()` 。（常用）

- 使用对象表达式， `var obj = Object()` 。

> 更多方式请看 [前端 - JavaScript 面向对象 创建对象.md](前端 - JavaScript 面向对象 创建对象.md)



### 使用 new 和构造函数

新对象可以使用 new 操作符后跟一个构造函数来创建。

构造函数本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的。

```js
var person = new Object();		// 创建 Object 对象
person.name = "Nicholas";
person.age = 29;
```



### 使用**对象字面量**表示法

另一种方式是使用**对象字面量**表示法。对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。

```js
var person = {
    name : "Nicholas",
    age : 29
};
```

在使用对象字面量语法时，属性名也可以使用字符串。数值属性名会自动转换为字符串。

```js
var person = {
    "name" : "Nicholas",
    "age" : 29,
    5 : true
};
```

使用对象字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象。

```js
var person = {}; 	// 与 new Object() 相同
person.name = "Nicholas";
person.age = 29;
```

推荐使用对象字面量方法定义对象。因为这种语法要求的代码量少，而且能够给人封装数据的感觉。实际上，对象字面量也是向函数传递大量可选参数的首选方式。



## **访问对象属性**

在 JavaScript 中，有两种访问对象属性的方法：

- 点表示法：通常，除非必须使用变量来访问属性，否则建议使用点表示法。

  ```js
  alert(person.name); 	// "Nicholas"，点表示法
  ```

- 方括号表示法：主要优点是可以通过变量来访问属性。

  ```js
  var propertyName = "name";
  alert(person[propertyName]); //"Nicholas"
  ```

  如果属性名中包含会导致语法错误的字符，或者属性名使用的是关键字或保留字，也可以使用方括号表示法。

  ```js
  // 由于"first name"中包含一个空格，所以不能使用点表示法来访问它。
  person["first name"] = "Nicholas";
  ```





## 添加属性

对于创建的对象，可以用点语法或者中括号语法为对象添加属性或者方法。

```js
obj["name"] = "Nicholas" 	// 方括号表示法
obj.name = "Nicholas"		// 点表示法
```



## 删除属性

 **`delete` 操作符**用于删除对象中的某个属性，但不能删除变量、函数等。如果没有指向这个属性的引用，那它最终会被释放。成功删除的时候回返回 `true`，否则返回 `false`。

```js
delete object.property 
delete object['property']
```

如果是属性是一个自己不可配置的属性，非严格模式返回 `false`。严格模式下会抛出 [`TypeError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypeError) 或者 [`SyntaxError`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/SyntaxError)。

```js
var Employee = {};
Object.defineProperty(Employee, 'name', {configurable: false});
console.log(delete Employee.name);  // returns false
```

删除一个数组元素时，数组的长度不受影响。

```js
var trees = ["redwood","bay","cedar"];
delete trees[1];
console.log(trees);	// ['redwood',<1 empty item>,'cedar']
console.log(trees[1],trees.length);	// undefined  3
if (3 in trees) {
   // 这里不会执行
}
```

让一个数组元素继续存在但是其值是 `undefined`，那么可以将 `undefined` 赋值给这个元素而不是使用 `delete`。

```js
var trees = ["redwood","bay","cedar"];
trees[1] = undefined;
if (3 in trees) {
   // 这里会被执行
}
```







