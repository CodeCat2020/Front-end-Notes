

# 流程控制语句

## **if 语句**

> if (condition) statement1 else statement2

condition 可以是任意表达式，表达式的结果不一定是布尔值。ES 会自动调用 Boolean() 转换函数将结果转换为布尔值。

```js
if (i > 25) {
	alert("Greater than 25.");
} else if (i < 0) {
	alert("Less than 0.");
} else {
	alert("Between 0 and 25, inclusive.");
}
```



## 循环结构



- do-while，循环体内的代码至少会被执行一次
- while，循环体内的代码有可能永远不会被执行。
- for，循环体内的代码有可能永远不会被执行。
- for-in
- for-of（ES6）



### **do-while 语句**

> do {statement} while (expression);

后测试循环语句，即只有在循环体中的代码执行之后，才会测试出口条件。

在对条件表达式求值之前，循环体内的代码至少会被执行一次。



### **while 语句**

> while(expression) statement

前测试循环语句，在循环体内的代码被执行之前，对出口条件求值。因此，循环体内的代码有可能永远不会被执行。



### **for 语句**

> for (initialization; expression; post-loop-expression) statement

前测试循环语句，但它具有在执行循环之前初始化变量和定义循环后要执行的代码的能力。

使用 while 循环做不到的，使用 for 循环同样也做不到。for 循环只是把与循环有关的代码集中在了一个位置。

由于 ES 中不存在块级作用域，因此在循环内部定义的变量也可以在外部访问到。

```js
var count = 10;
for (var i = 0; i < count; i++){
	alert(i);
}
alert(i); //10
```

for 语句中的初始化表达式、控制表达式和循环后表达式都是可选的。

```js
for (;;) { // 无限循环
	doSomething();
}
```

只给出控制表达式实际上就把 for 循环转换成了 while 循环：

```js
var count = 10;
var i = 0;
for (; i < count; ){
    alert(i);
    i++;
}
```



### **for-in 语句**

> for (property in expression) statement

一种精准的迭代语句，可以用来**枚举对象的属性**。下面是一个示例：

```js
var my_data = {a:’Ape’, b:’Banana’, c:’Citronella’};
for (var propName in my_data) {
	document.write(propName);
}
```

建议在使用 for-in 循环之前，先检测确认该对象的值不是 null 或 undefined。











## **label 语句**

> label: statement

使用 label 语句可以在代码中添加标签，以便将来使用。标签可以在将来由 break 或 continue 语句引用。加标签的语句一般都要与 for 语句等循环语句配合使用。



## **break 和 continue 语句**

break 和 continue 语句用于在循环中精确地控制代码的执行，都会立即退出循环。但退出后的位置不同：

- break ：从当前循环中退出。强制继续执行循环后面的语句。
- continue ：继续下一个循环语句。退出循环后会从循环的顶部继续执行。

break 和 continue 语句都可以与 label 语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套的情况下。

```js
var num = 0;
outermost:
for (var i=0; i < 10; i++) {
    for (var j=0; j < 10; j++) {
        if (i == 5 && j == 5) {
        	break outermost;
        }
        num++;
    }
}
alert(num); //55。如果两个循环都自然结束，num 的值应该是100
```

在上面的例子中，outermost 标签表示外部的 for 语句，添加这个标签的结果将导致 break 语句退出外部的 for 语句。

```js
var num = 0;
outermost:
for (var i=0; i < 10; i++) {
    for (var j=0; j < 10; j++) {
        if (i == 5 && j == 5) {
            continue outermost;
        }
        num++;
    }
}
alert(num); //95
```

在上面的情况下，continue 语句会强制继续执行循环——退出内部循环，执行外部循环。当 j 是 5 时，continue 语句执行，而这也就意味着内部循环少执行了 5 次，因此 num 的结果是 95。

虽然联用 break、continue 和 label 语句能够执行复杂的操作，但如果使用过度，也会给调试带来麻烦。因此，建议如果使用 label 语句，一定要使用描述性的标签，同时不要嵌套过多的循环。



## **with 语句**

> with (expression) statement;

with 语句的作用是将代码的作用域设置到一个特定的对象中，简化多次编写同一个对象的工作。

定义 with 语句的目的主要是为了简化多次编写同一个对象的工作。

```js
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;
```

上面几行代码都包含 location 对象。如果使用with 语句，可以把上面的代码改写成：

```js
with(location){
	var qs = search.substring(1);
	var hostName = hostname;
	var url = href;
}
```

> 由于大量使用 with 语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用 with 语句。



## **switch 语句**

```js
switch (expression) {
    case value: statement
    break;
    case value: statement
    break;
    case value: statement
    break;
    case value: statement
    break;
    default: statement
}
```

混合几种情形时，不要忘了在代码中添加注释，说明有意省略了 break 关键字。

```js
switch (i) {
    case 25:
    /* 合并两种情形 */
    case 35:
        alert("25 or 35");
        break;
    case 45:
        alert("45");
        break;
    default:
    	alert("Other");
}
```

ES 中的 switch 语句的特色

- 在 switch 语句中可以使用任何数据类型（在很多其他语言中只能使用数值）。
- 每个 case 的值不一定是常量，可以是变量，甚至是表达式。

```js
switch ("hello world") {
    case "hello" + " world":
        alert("Greeting was found.");
        break;
    case "goodbye":
        alert("Closing was found.");
        break;
    default:
    	alert("Unexpected message was found.");
}
```

switch 语句在比较值时使用的是全等操作符，因此不会发生类型转换（例如，字符串"10"不等于数值 10）。

