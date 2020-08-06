

# Array

Array 类型是一组值的有序列表，同时还提供了操作和转换这些值的功能。

ECMAScript 数组的每一项可以保存任何类型的数据。而且，数组的大小可以动态调整，即可以随着数据的添加自动增长以容纳新增数据。

数组最多可以包含 4 294 967 295 个项。超过这个上限值会发生异常。而创建一个初始大小与上限值接近的数组，则可能会导致运行时间超长的脚本错误。





JavaScript 中的数组可以存储不同类型的数据，数组中的数据也不一定是连续存储的（按照下标随机访问的效率不高），并且还能支持变长数组。

实际上，JavaScript 中数组的底层实现不依赖数据结构中的数组。JavaScript 中的数组会根据存储数据的不同，选择不同的实现方式。

- 如果数组中存储的是相同类型的数据，那么使用数据结构中数组来实现。也就是说，分配一块连续的内存空间来存储数据。
- 如果数组中存储的是不同类型的数据，那么使用类似散列表的结构来存储数据。也就是说，数据并不是连续存储在内存中的。这也是 JavaScript 数组支持存储不同类型数据的原因。
- 如果往一个存储了相同类型数据的数组中，插入一个不同类型的数据，那 JavaScript 会将底层的存储结构，从数组变成散列表。

JavaScript 还提供了另外一种数据类型 ArrayBuffer。而 ArrayBuffer 才符合标准的数据结构中数组的定义。它分配一片连续的内存空间，仅仅用来存储相同类型的数据。



## 1. 概述

### 创建方式

**方式一：使用 Array 构造函数**

使用 Array 构造函数创建数组。创建时可以给构造函数传递值：

- 传递一个数值，按照该数值创建包含给定项数的数组，该数值会自动变成 length 属性的值；
- 传递其他类型的参数，则会创建应该包含的项的数组。

```js
var arr1 = new Array();		// 定义一个空数组
var arr2 = new Array(3); 	// 创建一个包含 3 项的数组，length 值为 3
var arr3 = new Array("str1","str2"); // 创建一个包含 2 项，即"str1","str2"的数组
```

**方式二：数组字面量表示法**

数组字面量由一对包含数组项的方括号表示，多个数组项之间以逗号隔开。

```js
var arr4 = []; // 创建一个空数组
var arr5 = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
alert(arr4.length); //0
alert(arr5.length); //3
```

**不要在数组字面量的最后一项添加逗号**。

在省略值的情况下，省略值的项都将获得 undefined 值；这个结果与调用 Array 构造函数时传递项数在逻辑上是相同的。但是由于 IE 的实现与其他浏览器不一致，因此强烈建议不要使用这种语法。

下例中，在 IE 中，values 是一个包含 3 个项且每项的值分别为 1、2 和 undefined 的数组；在其他浏览器中，values 会成为一个包含 2 项且值分别为 1 和 2 的数组。

```js
var values = [1,2,]; // 不要这样！这样会创建一个包含 2 或 3 项的数组
var options = [,,,,,]; // 不要这样！这样会创建一个包含 5 或 6 项的数组
```



### 读取和设置数组



在读取和设置数组的值时，要使用方括号并提供相应值的基于 0 的数字索引。

- 如果索引小于数组中的项数，则返回对应项的值。设置数组的值也使用相同的语法，但会替换指定位置的值。
- 如果设置某个值的索引超过了数组现有项数，数组就会自动增加到该索引值加 1 的长度。

```js
var colors = ["red", "blue", "green"]; // 定义一个字符串数组
alert(colors[0]); // 显示第一项
colors[2] = "black"; // 修改第三项
colors[3] = "brown"; // 新增第四项
```



### **数组属性**

| 属性        | 描述                             |
| :---------- | :------------------------------- |
| constructor | 返回创建数组对象的原型函数。     |
| length      | 设置或返回数组元素的个数。       |
| prototype   | 允许你向数组对象添加属性或方法。 |



**length 属性**

数组的项数保存在其 length 属性中，这个属性始终会返回 0 或更大的值。

length 属性不是只读的。通过设置这个属性，可以从数组的末尾移除项或向数组中添加新项。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含3 个字符串的数组
colors.length = 2;
console.log(
	colors,				// ["red", "blue"]
    colors.length,		// 2
    colors[2],			// undefined。数组长度为2，没有第三项。
)
```

如果将其 length 属性设置为大于数组项数的值，则新增的每一项都会取得 undefined 值。此时，数组会重新计算其长度值，即长度值等于最后一项的索引加 1。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含3 个字符串的数组
colors[99] = "pink";
console.log(
	colors.length,	// 100
    colors[98],		// undefined。新增的项取得 undefined 值。
);
```

利用 length 属性也可以方便地在数组末尾添加新项。由于数组最后一项的索引始终是 length-1，因此下一个新项的位置就是 length。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含3 个字符串的数组
colors[colors.length] = "orange"; //（在位置3）添加一种颜色
colors[colors.length] = "brown"; //（在位置4）再添加一种颜色
```





### **二维数组**

可以把二维数组看成一组盒子，每个盒子里还可以放多个盒子。

```js
var myarr = [[0 , 1 , 2 ],[1 , 2 , 3]];
console.log(myarr[0][1]); 	// 输出1。其中 0 表示行，1表示列。
```



### 清空数组

- `arr.length=0`，最高效。
- `arr.splice(0,arr.length)`
- `arr=[]`：将一个新的数组的引用赋值给变量，其他引用并不受影响。 这意味着以前数组的内容被引用的话将依旧存在于内存中，将导致内存泄漏。









## 2. 检测数组

> 判断某个对象是不是数组：https://www.cnblogs.com/fogwind/p/5884684.html
>
> 如何判断一个对象是不是数组类型：https://www.cnblogs.com/peerless1029/p/9950005.html





- instanceof
- Array. isArray(obj)，可靠
- Object. prototype.toString.call(obj)==="[object Array]"，可靠

```js
console.log(
    typeof [],				// "object"，typeof 不能判断数组
	[] instanceof Object,	// true
    [] instanceof Array,	// true
    Array.isArray([]),		// true
	Object.prototype.toString.call([]),	// "[object Array]"
);							
```

可靠的方法：先检验本地是否有 `Array.isArray` 函数，没有就执行后面的方法检测。

```js
function isArray(obj){
    return Array.isArray(obj) || Object.prototype.toString.call(obj) === '[object Array]';
}
```



**测试用例**

以下用例中，obj1、obj6 属于 Array 类型；obj2、obj4 属于 Object 类型；obj3、obj5 属于 Function 类型。

```js
var obj1 = [],obj2 = {},obj3 = function(){},obj4 = {};
obj4.__proto__ = obj1;		// 改变了 obj4 的原型指向

var frame = document.createElement("iframe");// 创建一个框架
document.body.appendChild(frame);
var obj5 = window.frames[0].Array;	// 取得框架全局执行环境中的 Array 构造函数
var obj6 = new obj5();				// 在框架全局执行环境中创建一个数组 obj6
```



### instanceof

instanceof 操作符可以来表示实例是否属于某个构造函数创建的。

对于一个网页，或者一个全局作用域而言，使用 instanceof 操作符能得到满意的结果：

```js
console.log(
    obj1 instanceof Array,
    obj2 instanceof Array,
    obj3 instanceof Array,
    obj4 instanceof Array
);
//true false false true
console.log(Array.isArray(obj4));	// false
```

但是，instanceof 存在两个问题。上例中，因为改变了 obj4 的原型指向导致使用 instanceof 字符判断出 obj4 也为数组类型了。

第二个问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。

```js
console.log(obj6 instanceof Array); // 在当前页面的执行环境中，返回false。
console.log(Array.isArray(obj6)); 	// true
```



### Array.prototype.isPrototypeOf()

使用原型对象判断，instanceof 的问题仍存在。

```js
console.log(
	Array.prototype.isPrototypeOf(obj1),
    Array.prototype.isPrototypeOf(obj2),
    Array.prototype.isPrototypeOf(obj3),
    Array.prototype.isPrototypeOf(obj4),
    Array.prototype.isPrototypeOf(obj6),
);
// true false false true false
```



### Array.isArray()

为了解决上述问题，ES 5 新增了 **Array.isArray()** 方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的。

```js
if (Array.isArray(value)){
	//对数组执行某些操作
}
```

支持 Array.isArray() 方法的浏览器有 IE9+、Firefox 4+、Safari 5+、Opera 10.5+ 和 Chrome。



### Object.prototype.toString.call()

使用 Object.prototype 上的原生 toString() 方法判断。输入一个 obj，返回一个 `[object NativeConstructorName]` 格式的字符串。

原理：每个类在内部都有一个 `[[Class]]` 属性，这个属性中就指定了上述字符串中的构造函数名。一旦创建，无法修改。但是数组类型等内置类型重写了 toString 方法，直接调用数组对象的方法，不在返回 class。使用 call 替换 this 为指定对象调用 Object 原型上的 toString 方法即可。

该方法不能检测非原生构造函数的函数名，开发人员定义的任何构造函数都将返回 `[object Object]`。

```js
console.log(
    Object.prototype.toString.call(obj1),	//[object Array]
    Object.prototype.toString.call(obj2),	//[object Object]
    Object.prototype.toString.call(obj3),	//[object Function]
    Object.prototype.toString.call(obj4),	//[object Object]
    Object.prototype.toString.call(obj5),	//[object Function]
    Object.prototype.toString.call(obj6),  	//[object Array]
);

function Person() {
    this.name=name;
}
var n = new Person();
console.log(
    Object.prototype.toString.call(n),	// [object Object]
    console.log(n instanceof Function),	// false
);
```



## 3. 数组方法

### **3.1 转换方法**

#### **toString() 和 valueOf()** 

 toString() 返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串。valueOf() 返回的还是数组。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含3 个字符串的数组
console.log(
    colors.toString(),	// 字符串："red,blue,green"
    colors.valueOf(),	// 数组：["red", "blue", "green"]
    colors,				// ["red", "blue", "green"]
);
```

####  **toLocaleString()**

toLocaleString() 方法也会创建一个数组值的以逗号分隔的字符串。

```js
console.log(
    colors.toLocaleString(),	// 字符串："red,blue,green"
    colors,						// ["red", "blue", "green"]
);
```

与 toString() 方法唯一的不同之处在于，为了取得每一项的值，其调用的是每一项的 toLocaleString() 方法，而不是 toString() 方法。

```js
var person1 = {
    toLocaleString : function () {
    	return "Nikolaos";
    },
    toString : function() {
    	return "Nicholas";
    }
};
var person2 = {
    toLocaleString : function () {
    	return "Grigorios";
    },
    toString : function() {
    	return "Greg";
    }
};
var people = [person1, person2];
alert(people); 					// Nicholas,Greg
alert(people.toString()); 		// Nicholas,Greg
alert(people.toLocaleString()); // Nikolaos,Grigorios
```

#### **join()**

> *arrayObject.join(分隔符)*



使用 join() 方法，可以使用不同的分隔符来构建这个字符串。join() 方法只接收一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串，不改变原数组。

```js
var colors = ["red", "green", "blue"];
console.log(
	colors.join(","),	//red,green,blue
    colors.join("||"),	//red||green||blue
    colors,				//["red", "green", "blue"]
);
```



### **3.2 栈方法**





ECMAScript 数组提供了一种让数组的行为类似于其他数据结构的方法。

- push() 方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。
- pop() 方法则从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

```js
var colors = new Array(); 				// 创建一个数组
var count = colors.push("red", "green"); // 推入两项
alert(count); 	// 2

var item = colors.pop(); 	// 取得最后一项
alert(item);		 		// "green"
alert(colors.length); 		// 1
```



### **3.3 队列方法**

shift() 方法能够移除数组中的第一个项并返回该项，同时将数组长度减 1。

结合使用 shift() 和 push() 方法，可以像使用队列一样使用数组。

```js
var colors = new Array(); 				 // 创建一个数组
var count = colors.push("red", "green"); // 推入两项
alert(count); 	// 2

var item = colors.shift(); // 取得第一项
alert(item); 			// "red"
alert(colors.length); 	// 1
```



与 shift() 的用途相反，unshift() 能在**数组前端**添加任意个项，并返回新数组的长度。

因此，同时使用 unshift() 和 pop() 方法，可以从相反的方向来模拟队列，即在数组的前端添加项，从数组末端移除项。

```js
var colors = new Array(); // 创建一个数组
var count = colors.unshift("red", "green"); // 推入两项
alert(count); //2

var item = colors.pop();	// 取得最后一项
alert(item); 				// "green"
alert(colors.length); 		// 1
```

> IE7 及更早版本对 JavaScript 的实现中存在一个偏差，其 unshift() 方法总是返回undefined 而不是数组的新长度。IE8 在非兼容模式下会返回正确的长度值。



### **3.4 重排序方法**

#### **reverse()** 

> arrayObject.reverse()

reverse() 和 sort() 方法的返回值是经过排序之后的数组，都会改变原数组。reverse() 方法会反转数组项的顺序。reverse() 不够灵活，因此才有了 sort() 方法。

```js
var values = [0, 1, 5, 10, 15];
values.reverse();
console.log(values); // [15, 10, 5, 1, 0]
```

#### **sort()** 

> *arr.sort([compareFunction])*

sort() 方法用原地算法对数组的元素进行排序，并返回数组。由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。

为了实现排序，sort() 方法会调用每个数组项的 toString() 转型方法，然后比较得到的字符串，按 unicode码排列。默认情况下，sort() 方法按升序排列数组项。

```js
var values = [0, 1, 5, 10, 15];
values.sort();
alert(values); //0,1,10,15,5
```

sort() 方法可以接收一个比较函数作为参数，以便指定哪个值位于哪个值的前面。比较函数接收两个参数。

-  如果第一个参数应该位于第二个之前，则返回一个负数。
-  如果两个参数相等，则返回 0。
-  如果第一个参数应该位于第二个之后，则返回一个正数。

下面的比较函数按升序排列，适用于大多数数据类型，只要将其作为参数传递给 sort() 方法即可。

```js
// 比较函数，升序
function compare(value1, value2) {
    if (value1 < value2) {
    	return -1;
    } else if (value1 > value2) {
    	return 1;
    } else {
    	return 0;
    }
}
values.sort(compare);
alert(values); //0,1,5,10,15
```

可以通过比较函数产生降序排序的结果，交换比较函数返回的值即可。

```js
// 降序
function compare(value1, value2) {
    if (value1 < value2) {
    	return 1;
    } else if (value1 > value2) {
    	return -1;
    } else {
    	return 0;
    }
}
values.sort(compare);
alert(values); // 15,10,5,1,0
```



对于数值类型或者其 valueOf() 方法会返回数值类型的对象类型，由于比较函数通过返回一个小于零、等于零或大于零的值来影响排序结果，因此减法操作可以适当地处理所有这些情况。

升序：

```js
// 升序
function compare(value1, value2){
	return value1 - value2;		// 如果 value1 > value2，返回值 > 0，交换位置
}
```

降序：

```js
function compare(value1, value2){
	return value2 - value1;				// 降序
}
```



**对非 ASCII 字符排序**

一些非英语语言的字符串需要使用 [`String.localeCompare`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare)。这个函数可以将函数排序到正确的顺序。

```js
var items = ['réservé', 'premier', 'cliché', 'communiqué', 'café', 'adieu'];
items.sort(function (a, b) {
    return a.localeCompare(b);
});

// items is ['adieu', 'café', 'cliché', 'communiqué', 'premier', 'réservé']
```



`sort` 方法可以使用函数表达式方便地书写：

```js
var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
    return a - b;			// 也可以写成：numbers.sort((a, b) => a - b); 
});
console.log(numbers);		// [1, 2, 3, 4, 5]
```







### 3.5 操作方法



#### **concat()**

> *var new_array = old_array.concat(value1[, value2[, ...[, valueN]]])*

concat() 方法可以基于当前数组中的所有项创建一个新数组。不改变原来的数组，先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。

```js
var colors = ["red", "green", "blue"];
var colors2 = colors.concat("yellow", ["black", "brown"]);
console.log(
	colors,		// ["red", "green", "blue"]
    colors2,	// ["red", "green", "blue", "yellow", "black", "brown"]
);
```

#### **slice()**

> *arr.slice([begin[, end]])*

`slice()` 方法返回一个新的数组对象，这一对象是一个由 `begin` 和 `end` 决定的原数组的**浅拷贝**（包括 `begin`，不包括 `end`）。<u>原始数组不会被改变</u>。

- 如果只有一个参数时，返回从该参数指定位置开始到当前数组末尾的所有项。
- 如果有两个参数，返回起始和结束位置（不包括结束位置）之间的项。

```js
var colors = ["red", "green", "blue", "yellow", "purple"];
var colors2 = colors.slice(1);
var colors3 = colors.slice(1,4);
var colors4 = colors.slice(-4,-1);
var colors5 = colors.slice(4,1);
var colors5 = colors.slice(6);
console.log(
    colors2,	// ["green", "blue", "yellow", "purple"] 
    colors3,	// ["green", "blue", "yellow"]
    colors4,	// ["green", "blue", "yellow"]
    colors5,	// []
    colors6,	// []
    colors,		// ["red", "green", "blue", "yellow", "purple"]
);
```

注意：

- 可使用负值从数组的尾部选取元素。如果参数中有负数，则用数组长度加上该数来确定相应的位置。
- 如果结束位置小于起始位置或者起始位置大于数组长度，返回空数组。
- String.slice() 与 Array.slice() 相似。



#### **splice()**

> *array.splice(start[, deleteCount[, item1[, item2[, ...]]]])*



splice() 方法用于添加或删除数组中的元素，这种方法会改变原始数组。splice() 方法返回一个数组，该数组包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）。

splice() 方法的参数如下：

| 参数                  | 描述                                                         |
| :-------------------- | :----------------------------------------------------------- |
| *start*               | 必需。规定从何处添加/删除元素。 该参数是开始插入和（或）删除的数组元素的下标，必须是数字。 |
| *deleteCount*         | 可选。规定应该删除多少元素。必须是数字，但可以是 "0"。 如果未规定此参数，则删除从 index 开始到原数组结尾的所有元素。 |
| *item1*, ..., *itemX* | 可选。要添加到数组的新元素                                   |

使用这种方法的方式则有如下 3 种：

- 删除：可以删除任意数量的项。

  - 指定 2 个参数，要删除的第一项的位置和要删除的项数。如果要删除的项数大于数组长度，删除从指定位置开始到数组末尾的项。

    ```js
    var colors = ["red", "green", "blue","orange"];
    console.log(colors.splice(0,1)); 	// 删除第一项，返回 ['red']
    console.log(colors); 	// 原数组剩下三项 ['green','blue','orange']
    console.log(colors.splice(1,1)); 	// 删除第二项
    ```

  - 指定 1 个参数，删除从指定位置开始到数组末尾的项。

    ```js
    var colors = ["red", "green", "blue","orange"];
    console.log(
        colors.splice(1),	// ["blue", "orange"]，删除第二项后面的项。
    	colors,				// ["green"]，原数组剩下一项。
    );	
    ```

- 插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、0（要删除的项数）和要插入的项。如果要插入多个项，可以再传入任意多个项。

  ```js
  colors = ["red", "green", "blue","orange"];
  removed = colors.splice(1, 0, "yellow", "orange"); // 从位置 1 开始插入两项
  alert(colors); // red,yellow,orange,green,blue,orange
  alert(removed); // 返回的是一个空数组
  ```

  如果没有中间的参数：

  ```js
  colors = ["red", "green", "blue","orange"];
  removed = colors.splice(1, "yellow", "orange"); 
  alert(colors); // red,orange,green,blue,orange
  alert(removed); // 返回的是一个空数组
  ```

- 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数（不为 0）和要插入的任意数量的项。插入的项数不必与删除的项数相等。

  ```js
  colors = ["red", "green", "blue","orange"];
  removed = colors.splice(1, 1, "red", "purple"); // 先删除位置1的项，然后从位置1开始插入两项
  alert(colors); // red,red,purple,blue,orange
  alert(removed); // green，返回的数组中只包含一项
  ```







### 3.6 位置方法

**indexOf() 和 lastIndexOf()**

> *arr.indexOf(searchElement[, fromIndex])*
>
> *arr.lastIndexOf(searchElement[, fromIndex])*

ES 5 为数组实例添加了两个位置方法：indexOf() 和 lastIndexOf()。这两个方法都接收两个参数：要查找的项和表示查找起点位置的索引。其中 indexOf() 方法从数组的开头开始向后查找，lastIndexOf() 方法则从数组的末尾开始向前查找。

这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回 -1。在比较第一个参数与数组中的每一项时，会使用全等操作符；也就是说，要求查找的项必须严格相等。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
alert(numbers.indexOf(4)); 		// 3。从数组开头开始找，numbers[3]是4。
alert(numbers.lastIndexOf(4)); 	// 5。从数组末尾开始找，numbers[5]是4。

alert(numbers.indexOf(4, 4)); 	// 5。从索引为4的位置开始找，numbers[5]是4。
alert(numbers.lastIndexOf(4, 4)); //3。从末尾向前索引为4的位置开始找，numbers[3]是4。
var person = { name: "Nicholas" };
var people = [{ name: "Nicholas" }];
var morePeople = [person];
alert(people.indexOf(person)); 		// -1。没找到。
alert(morePeople.indexOf(person)); 	// 0。在索引为 0 的位置找到。
```

可以用来检查数组是否包含某个值：

```js
if (arr.indexOf(el) !== -1) {
  // ...
}
```



### 3.7 迭代方法

> *array.every(function(currentValue,index,arr), [thisValue])*

ES 5 为数组定义了 5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响 this 的值。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。

根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。以下是这5 个迭代方法的作用。

- every()：对数组中的每一项运行给定函数，如果该函数对**每一项**都返回 true，则<u>返回 true</u>。
- filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的<u>数组</u>。
- forEach()：对数组中的每一项运行给定函数。这个方法<u>没有返回值</u>。
- map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的<u>数组</u>。
- some()：对数组中的每一项运行给定函数，如果该函数对**任一项**返回 true，则返回 true。

以上方法都不会修改数组中的包含的值。





####  **every() 和 some()**





最相似的是 every() 和 some()，它们的参数和返回类型相同，且都用于查询数组中的项是否满足某个条件。

- some()：如果该函数对**每一项**都返回 true，则返回 true。
- every()：如果该函数对**任一项**返回 true，则返回 true。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var everyResult = numbers.every(function(item, index, array){
	return (item > 2);
});
alert(everyResult); 	// false。并不是每一项都大于2。
var someResult = numbers.some(function(item, index, array){
	return (item > 2);
});
alert(someResult); 		// true。存在一些大于2的项。
```



#### **filter()**

filter() 函数利用指定的函数确定是否在返回的数组中包含某一项。例如，要返回一个所有数值都大于 2 的数组。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var filterResult = numbers.filter(function(item, index, array){
	return (item > 2);
});
alert(filterResult); //[3,4,5,4,3]
```

#### **map()** 

map() 方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。

语法：

```js
var new_array = arr.map(function callback(currentValue[, index[, array]]) {
    // Return element for new_array 
}[, thisArg])
```

参数：

- callback：生成新数组元素的函数，使用三个参数：
  - `currentValue`：`callback` 数组中正在处理的当前元素。
  - `index`：可选，`callback` 数组中正在处理的当前元素的索引。
  - `array`：可选，`map` 方法调用的数组。

- `thisArg`：可选，执行 `callback` 函数时值被用作 `this`。

例如，可以给数组中的每一项乘以 2，然后返回这些乘积组成的数组。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var mapResult = numbers.map(function(item, index, array){
	return item * 2;
});
alert(mapResult); //[2,4,6,8,10,8,6,4,2]
```

求数组中每个元素的平方根

```js
var numbers = [1, 4, 9];
var roots = numbers.map(Math.sqrt);
// roots的值为[1, 2, 3], numbers的值仍为[1, 4, 9]
```

使用一个包含对象的数组来重新创建一个格式化后的数组。

```js
var kvArray = [{key: 1, value: 10}, 
               {key: 2, value: 20}, 
               {key: 3, value: 30}];

var reformattedArray = kvArray.map(function(obj) { 
    var rObj = {};
    rObj[obj.key] = obj.value;
    return rObj;
});
// reformattedArray 数组为： [{1: 10}, {2: 20}, {3: 30}], kvArray 数组未被修改
```

在一个 `String` 上使用 map 方法获取字符串中每个字符所对应的 ASCII 码组成的数组：

```js
var map = Array.prototype.map
var a = map.call("Hello World", function(x) { 
  return x.charCodeAt(0); 
})
// a的值为[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]
```

去遍历用 `querySelectorAll `得到的动态对象集合。

```js
var elems = document.querySelectorAll('select option:checked');
var values = Array.prototype.map.call(elems, function(obj) {
  return obj.value;
});
```

通常情况下，`map` 方法中的 `callback` 函数只需要接受一个参数，就是正在被遍历的数组元素本身。但这并不意味着 `map` 只给 `callback` 传了一个参数。

**特殊案例**

```js
["1", "2", "3"].map(parseInt);	// 期望输出 [1, 2, 3], 实际输出 [1, NaN, NaN]
// 执行过程 parseInt(string, radix) -> map(parseInt(value, index))
// parseInt('1',0); 	// radix 为 0，根据十进制来解析，所以结果为 1
// parseInt('2',1); 	// 2 不是 1 进制数，所以结果为 NaN；
// parseInt('3',2);		// 3 不是 2 进制数，所以结果为 NaN。
```

因为 parseInt 需要两个参数， map 传递了 3 个参数，这里 parseInt 省略了第三个参数。在 parseInt 中，对应的 radix 不合法或者参数不是基于 radix 的数将导致解析失败。

解决方案

```js
function returnInt(element) {
    return parseInt(element, 10);
}
console.log(
	['1', '2', '3'].map(returnInt), 	// [1, 2, 3]
    ['1', '2', '3'].map( str => parseInt(str) ),
    ['1', '2', '3'].map(Number), 		// [1, 2, 3]，避免"gotcha"
    ['1.1', '2.2e2', '3e300'].map(Number),	// [1.1, 220, 3e+300]
    ['1.1', '2.2e2', '3e300'].map( str => parseInt(str) ), // [1, 2, 3]
);
```

Mapping 含 undefined 的数组

```js
var numbers = [1, 2, 3, 4];
var filteredNumbers = numbers.map(function(num, index) {
  if(index < 3) {
     return num;
  }
});
console.log(filteredNumbers);	// [ 1, 2, 3, undefined ]
```



#### **forEach()**

> *arr.forEach(callback(currentValue [, index [, array]])[, thisArg])*

forEach() 方法对数组的每个元素执行一次给定的函数。这个方法没有返回值，本质上与使用 for 循环迭代数组一样。不能将 arr.foreach() 像其他数组迭代方法那样赋值给某一个变量。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
numbers.forEach(function(item, index, array){
	//执行某些操作
});
```



除了抛出异常以外，没有办法中止或跳出 `forEach()` 循环。



将 for 循环转换为 forEach

```js
const items = ['item1', 'item2', 'item3'];
const copy = [];

// before
for (let i=0; i<items.length; i++) {
    copy.push(items[i]);
}

// after
items.forEach(function(item){
    copy.push(item);
});
```





### **3.8 归并方法**

ES 5 还新增了两个归并数组的方法：reduce() 和 reduceRight()。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。不会影响原数组。

- reduce() 方法从数组的第一项开始，逐个遍历到最后。
- reduceRight() 从数组的最后一项开始，向前遍历到第一项。

使用 reduce() 还是 reduceRight()，主要取决于要从哪头开始遍历数组。除此之外，它们完全相同。

####  **reduce()** 

> *arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])*



reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

参数

- `callback`：执行数组中每个值 (如果没有提供 `initialValue` 则第一个值除外)的函数，包含四个参数：
  - **`accumulator`**：累计器累计回调的返回值；它是上一次调用回调时返回的累积值，或`initialValue`。
  - `currentValue`：数组中正在处理的元素。
  - `index` ：可选，数组中正在处理的当前元素的索引。 如果提供了`initialValue`，则起始索引号为 0，否则从索引 1 起始。
  - `array`：可选，调用 `reduce()` 的数组
- `initialValue`：可选。作为第一次调用 `callback` 函数时的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。



使用 reduce() 方法可以执行求数组中所有值之和的操作。

```js
var values = [1,2,3,4,5];
var sum = values.reduce(function(prev, cur, index, array){
	return prev + cur;	// 第一次执行回调函数，prev 是 1，cur 是 2
});
alert(sum); // 15
```





#### reduceRight() 

reduceRight() 的作用类似，只不过方向相反而已。

```js
var values = [1,2,3,4,5];
var sum = values.reduceRight(function(prev, cur, index, array){
	return prev + cur;	// 第一次执行回调函数，prev 是 5，cur 是 4。
});
alert(sum); //15
```





### 3.9 汇总

原生 JS 操作数组的方法。

| 方法                                                         | 描述                                                 | 用法                       | 改变原数组 |
| :----------------------------------------------------------- | :--------------------------------------------------- | -------------------------- | ---------- |
| [concat()](https://www.runoob.com/jsref/jsref-concat-array.html) | 连接两个或更多的数组，并返回新数组。                 | arr1.concat(arr2,...,arrN) | 否         |
| [copyWithin()](https://www.runoob.com/jsref/jsref-copywithin.html)（ES6） | 从数组的指定位置拷贝元素到数组的另一个指定位置中。   |                            |            |
| [entries()](https://www.runoob.com/jsref/jsref-entries.html)（ES6） | 返回数组的可迭代对象。                               |                            |            |
| [every()](https://www.runoob.com/jsref/jsref-every.html)     | 检测数值元素的每个元素是否都符合条件。               |                            | 否         |
| [fill()](https://www.runoob.com/jsref/jsref-fill.html)（ES6） | 使用一个固定值来填充数组。                           |                            |            |
| [filter()](https://www.runoob.com/jsref/jsref-filter.html)   | 检测数值元素，并返回符合条件所有元素的数组。         |                            | 否         |
| [find()](https://www.runoob.com/jsref/jsref-find.html)（ES6） | 返回符合传入测试（函数）条件的数组元素。             |                            |            |
| [findIndex()](https://www.runoob.com/jsref/jsref-findindex.html)（ES6） | 返回符合传入测试（函数）条件的数组元素索引。         |                            |            |
| [forEach()](https://www.runoob.com/jsref/jsref-foreach.html) | 数组每个元素都执行一次回调函数。                     |                            | 否         |
| [from()](https://www.runoob.com/jsref/jsref-from.html)（ES6） | 通过给定的对象中创建一个数组。                       |                            |            |
| [includes()](https://www.runoob.com/jsref/jsref-includes.html)（ES6） | 判断一个数组是否包含一个指定的值。                   |                            |            |
| [indexOf()](https://www.runoob.com/jsref/jsref-indexof-array.html) | 搜索数组中的元素，并返回它所在的位置。               |                            | 否         |
| [isArray()](https://www.runoob.com/jsref/jsref-isarray.html) | 判断对象是否为数组。                                 |                            | 否         |
| [join()](https://www.runoob.com/jsref/jsref-join.html)       | 指定分隔符，把数组的所有元素放入一个字符串。         | arr1.concat("-")           | 否         |
| [keys()](https://www.runoob.com/jsref/jsref-keys.html)（ES6） | 返回数组的可迭代对象，包含原始数组的键(key)。        |                            |            |
| [lastIndexOf()](https://www.runoob.com/jsref/jsref-lastindexof-array.html) | 搜索数组中的元素，并返回它最后出现的位置。           |                            | 否         |
| [map()](https://www.runoob.com/jsref/jsref-map.html)         | 通过指定函数处理数组的每个元素，并返回处理后的数组。 |                            | 否         |
| [pop()](https://www.runoob.com/jsref/jsref-pop.html)         | 删除数组的最后一个元素并返回删除的元素。             |                            | 是         |
| [push()](https://www.runoob.com/jsref/jsref-push.html)       | 向数组的末尾添加一个或更多元素，并返回新的长度。     |                            | 是         |
| [reduce()](https://www.runoob.com/jsref/jsref-reduce.html)   | 将数组元素计算为一个值（从左到右）。                 |                            | 否         |
| [reduceRight()](https://www.runoob.com/jsref/jsref-reduceright.html) | 将数组元素计算为一个值（从右到左）。                 |                            | 否         |
| [reverse()](https://www.runoob.com/jsref/jsref-reverse.html) | 反转数组的元素顺序。                                 | arr.reverse()              | 是         |
| [shift()](https://www.runoob.com/jsref/jsref-shift.html)     | 删除并返回数组的第一个元素。                         |                            | 是         |
| [slice()](https://www.runoob.com/jsref/jsref-slice-array.html) | 选取数组的的一部分，并返回一个新数组。               | arr.slice(start,[end])     | 否         |
| [some()](https://www.runoob.com/jsref/jsref-some.html)       | 检测数组元素中是否有元素符合指定条件。               |                            | 否         |
| [sort()](https://www.runoob.com/jsref/jsref-sort.html)       | 对数组的元素进行排序。                               | arr.sort([方法函数])       | 是         |
| [splice()](https://www.runoob.com/jsref/jsref-splice.html)   | 从数组中添加或删除元素。                             |                            | 是         |
| [toString()](https://www.runoob.com/jsref/jsref-tostring-array.html) | 把数组转换为字符串，并返回结果。                     |                            | 否         |
| [unshift()](https://www.runoob.com/jsref/jsref-unshift.html) | 向数组的开头添加一个或更多元素，并返回新的长度。     |                            | 是         |
| [valueOf()](https://www.runoob.com/jsref/jsref-valueof-array.html) | 返回数组对象的原始值。                               |                            | 否         |



是否更改原有数组：

会改变原数组的方法：栈方法、队列方法、重排序方法（**sort**）、**splice()** 。

不会改变原数组的方法：转换方法、**concat()**、slice()、位置方法、迭代方法（**map**）、归并方法。







# 参考资料

[Array.prototype.sort() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

[[译] V8引擎中的排序 - 知乎](https://zhuanlan.zhihu.com/p/55338902)

[Array.prototype.map() - MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

[详解数据结构中的“数组”与编程语言中的“数组”的区别和联系](https://mp.weixin.qq.com/s/E-c41h2v_AfffrlAQpkyLg)