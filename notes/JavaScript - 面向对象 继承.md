# 继承

许多 OO 语言都支持两种继承方式：接口继承和实现继承。接口继承只继承方法签名（接受的参数的类型和数量），实现继承则继承实际的方法。

由于函数没有签名，ECMAScript 无法实现接口继承，只支持实现继承。



## 1. 原型链

JavaScript 主要通过原型链实现继承。其基本思想是利用原型让一个引用类型（子类型）继承另一个引用类型（父类型）的属性和方法。这一点与基于类的继承很相似。

构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。

假如**让原型对象等于另一个类型的实例**，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立，如此层层递进，就构成了实例与原型的链条。这就是原型链的基本概念。



实现原型链有一种基本模式，其代码大致如下。

```js
function SuperType(){
	this.property = true;
}
SuperType.prototype.getSuperValue = function(){
	return this.property;
};

function SubType(){
	this.subproperty = false;
}
// SubType 继承了SuperType
// 通过创建 SuperType 的实例，并将该实例赋给 SubType.prototype 实现
SubType.prototype = new SuperType();
// 添加新方法
SubType.prototype.getSubValue = function (){
	return this.subproperty;
};
var instance = new SubType();
alert(instance.getSuperValue()); // true
```

这个例子中的实例以及构造函数和原型之间的关系：

<div align="center"> <img src="pics/前端 - JavaScript 面向对象 继承 原型链2.png"/> </div><br>

要注意 instance.constructor 现在指向的是 SuperType，这是因为原来 SubType.prototype 中的 constructor 被重写了。

instance.getSuperValue() 会经历三个搜索步骤：1）搜索实例；2）搜索SubType.prototype；3）搜索SuperType.prototype，最后一步才会找到该方法。

在找不到属性或方法的情况下，搜索过程总是要一环一环地前行到原型链末端才会停下来。



### **默认的原型**

所有引用类型默认都继承了 Object。而这个继承也是通过原型链实现的。

所有函数的默认原型都是 Object 的实例，因此默认原型都会包含一个内部指针，指向 Object.prototype。这也是所有自定义类型都会继承 toString()、valueOf() 等默认方法的根本原因。

SubType 继承了 SuperType，而 SuperType 继承了 Object。当调用 instance.toString() 时，实际上调用的是保存在 Object.prototype 中的那个方法。





### Object 与 Function

- 当 new 一个函数的时候会创建一个对象，`被创建对象.__proto__ === 函数.prototype `。

- 一切函数都是由 Function 这个函数创建的，所以 `被创建的函数.__proto__ === Function.prototype`。
- 一切函数的原型对象都是由 Object 这个函数创建的，所以`一切函数.prototype.__proto__ === Object.prototype`。

- `Object.prototype.__proto__ === null`，说明原型链到 Object.prototype 终止。
- 表达式 `Function.prototype.__proto__.__proto__ === null` 的运行结果为 true。

```js
// 代码1
function People(){}
var p = new People();
console.log(
    p.constructor,			// [Function: People]
    p.__proto__,			// People {}
    // p.__proto__ === People.prototype
    p.__proto__ === p.constructor.prototype,	// true
    People.__proto__ === Function.prototype,	// true
    // People.prototype.__proto__ === Object.prototype
    p.__proto__.__proto__ === Object.prototype,	// true
    // Object.prototype.__proto__ === null
    p.__proto__.__proto__.__proto__ === null	// true
);


// 代码2
console.log(
	Function.__proto__ === Function.prototype,
	Object.__proto__ === Function.prototype,
	Function.prototype.__proto__ === Object.prototype,
);
// true true true

//代码3
console.log(
    // Function.__proto__ === Function.prototype
    Function instanceof Function,	
    // Function.__proto__.__proto__ === Function.prototype.__proto__ === Object.prototype
    Function instanceof Object,
    // Object.__proto__ === Function.prototype
    Object instanceof Function,
    // Object.__proto__.__proto__ === Function.prototype.__proto__ === Object.prototype
    Object instanceof Object,
);
// true true true true
```

<div align="center"> <img src="pics/JavaScript Object原型链继承.jpg"/> </div><br>

构造函数与实例

构造函数返回的是一个对象，是 Object 的一个实例，没有继承 Function，所以无法访问 Function 原型里面的属性。

构造函数是 Function 对象的一个实例，可以访问到 Function 原型里面的属性。在 JavaScript 里面，所有对象都是 Object 的实例，所以构造函数可以访问到 Object 原型里面的属性。

```js
Function.prototype.a = 'a';
Object.prototype.b = 'b';
function Person(){};			// Person 多继承
var p = new Person();			// p 是对象，只能继承于 Object.prototype
console.log('p.a: '+ p.a); // p.a: undefined
console.log('p.b: '+ p.b); // p.b: b  为什么？
console.log('Person.a: '+ Person.a); // Person.a: a
console.log('Person.b: '+ Person.b); // Person.b: b
```





### **确定原型和实例的关系**





如何判断一个对象是否属于某个类？

使用 instanceof 关键字，判断一个对象是否是类的实例化对象；使用 constructor 属性，判断一个对象是否是类的构造函数。



第一种方式是使用 instanceof 操作符，只要用这个操作符来测试实例与原型链中出现过的构造函数，结果就会返回 true。

由于原型链的关系，上例中 instance 是 Object、SuperType 或 SubType 中任何一个类型的实例。

```js
alert(instance instanceof Object); 		// true
alert(instance instanceof SuperType); 	// true
alert(instance instanceof SubType); 	// true
```

第二种方式是使用 isPrototypeOf() 方法。只要是原型链中出现过的原型，都可以说是该原型链所派生的实例的原型。

```js
alert(Object.prototype.isPrototypeOf(instance)); 	// true
alert(SuperType.prototype.isPrototypeOf(instance)); // true
alert(SubType.prototype.isPrototypeOf(instance)); 	// true
```



### **谨慎的定义方法**

给原型添加方法的代码一定要放在替换原型的语句之后。

在通过原型链实现继承时，不能使用对象字面量创建原型方法。因为这样做就会重写原型链。



### **原型链的问题**

原型链最主要的问题来自包含引用类型值的原型。对象实例会共享所有继承的属性和方法，因此不适宜单独使用。

原型链的第二个问题是：在创建子类型的实例时，不能向超类型的构造函数中传递参数。没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。

有鉴于此，实践中很少会单独使用原型链。



## 2. 借用构造函数

解决包含引用类型值所带来问题的技术是借用构造函数（constructor stealing）（有时候也叫做伪造对象或经典继承）。基本思想相当简单，即**在子类型构造函数的内部调用超类型构造函数**。函数只是在特定环境中执行代码的对象，因此通过使用 apply() 和 call() 方法也可以在（将来）新创建的对象上执行构造函数。

这样就可以做到每个实例都具有自己的属性，同时还能保证只使用构造函数模式来定义类型。

```js
function SuperType(){
    this.colors = ["red", "blue", "green"];
}
function SubType(){
    // 继承了 SuperType，“借调”了超类型的构造函数
    SuperType.call(this);
}
var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); 	// "red,blue,green,black"
var instance2 = new SubType();
alert(instance2.colors); 	// "red,blue,green"
```

### **传递参数**

相对于原型链而言，借用构造函数有一个很大的优势，即可以在子类型构造函数中向超类型构造函数传递参数。

```js
function SuperType(name){
    this.name = name;
}
function SubType(){
    // 继承了 SuperType，同时还传递了参数
    SuperType.call(this, "Nicholas");
    // 实例属性
    this.age = 29;
}
var instance = new SubType();
alert(instance.name); 	// "Nicholas";
alert(instance.age); 	// 29
```

### **借用构造函数的问题**

无法避免构造函数模式存在的问题——方法都在构造函数中定义，无法实现函数复用。而且，在超类型的原型中定义的方法，对子类型而言也是不可见的，结果所有类型都只能使用构造函数模式。

考虑到这些问题，借用构造函数的技术也是很少单独使用的。



## 3. 组合继承

组合继承（combination inheritance），有时候也叫做伪经典继承，指的是将原型链和借用构造函数的技术组合到一块，从而发挥二者之长的一种继承模式。

实现思路是使用原型链继承共享的属性和方法，而通过借用构造函数继承实例属性。

```js
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
    alert(this.name);
};
function SubType(name, age){
    // 继承属性
    SuperType.call(this, name);
    this.age = age;
}
// 继承方法
SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;
SubType.prototype.sayAge = function(){
    alert(this.age);
};
var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors); 	// "red,blue,green,black"
instance1.sayName(); 		// "Nicholas";
instance1.sayAge(); 		// 29
var instance2 = new SubType("Greg", 27);
alert(instance2.colors); 	// "red,blue,green"
instance2.sayName(); 		// "Greg";
instance2.sayAge(); 		// 27
```

组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为 JavaScript 中最常用的继承模式。而且，instanceof 和 isPrototypeOf() 也能够用于识别基于组合继承创建的对象。



## 4. 原型式继承

道格拉斯·克罗克福德在 2006 年介绍了一种实现继承的方法，这种方法并没有使用严格意义上的构造函数。他的想法是借助原型可以**基于已有的对象**创建新对象，同时还不必因此创建自定义类型。为了达到这个目的，他给出了如下函数。

从本质上讲，object() 对传入其中的对象执行了一次浅复制。

```js
function object(o){
    function F(){}		// 先创建了一个临时性的构造函数
    F.prototype = o;	// 然后将传入的对象作为这个构造函数的原型
    return new F();		// 返回了这个临时类型的一个新实例
}
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
var anotherPerson = object(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");
alert(person.friends); 		// ['Shelby','Court','Van','Rob']
var yetAnotherPerson = object(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");
alert(person.friends); 		// ['Shelby','Court','Van','Rob','Barbie']
```

ECMAScript 5 新增 **`Object.create()`** 方法规范化了原型式继承。这个方法创建一个新对象，使用现有的对象来提供新创建的对象的 `__proto__`。

```
Object.create(proto[, propertiesObject])
```

这个方法接收两个参数：

- `proto`：新创建对象的原型对象。

- `propertiesObject`：可选。新对象定义额外属性的对象

  如果没有指定为 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)，则是要添加到新创建对象的不可枚举（默认）属性（即其自身定义的属性，而不是其原型链上的枚举属性）对象的属性描述符以及相应的属性名称。这些属性对应[`Object.defineProperties()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)的第二个参数。

在传入一个参数的情况下， Object.create() 与 object() 方法的行为相同。

Object.create() 方法的第二个参数与 Object.defineProperties() 方法的第二个参数格式相
同：每个属性都是通过自己的描述符定义的。以这种方式指定的任何属性都会覆盖原型对象上的同名属性。

```js
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
var anotherPerson = Object.create(person, {
    name: {
        value: "Greg"
    }
});
alert(anotherPerson.name); // "Greg"
```

支持 Object.create() 方法的浏览器有 IE9+、Firefox 4+、Safari 5+、Opera 12+ 和 Chrome。



## 5. 寄生式继承

寄生式（parasitic）继承与原型式继承紧密相关，并且同样也是由克罗克福德推广的。寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象。

以下代码示范了寄生式继承模式。

```js
function createAnother(original){
    var clone = object(original); 	// 通过调用函数创建一个新对象
    clone.sayHi = function(){ 		// 以某种方式来增强这个对象
        alert("hi");
    };
    return clone; 					// 返回这个对象
}
var person = {
    name: "Nicholas",
    friends: ["Shelby", "Court", "Van"]
};
var anotherPerson = createAnother(person);
anotherPerson.sayHi(); //"hi"
```

使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率；这一点与构造函数模式类似。



## 6. 寄生组合式继承

组合继承最大的问题就是无论什么情况下，都会调用两次超类型构造函数：一次是在创建子类型原型的时候，另一次是在子类型构造函数内部。

子类型最终会包含超类型对象的全部实例属性，但不得不在调用子类型构造函数时重写这些属性。

寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。其背后的基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，所需要的只是超类型原型的一个副本。本质上，就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型。

寄生组合式继承的基本模式如下所示。

```js
// 接收两个参数：子类型构造函数和超类型构造函数。
function inheritPrototype(subType, superType){
    var prototype = object(superType.prototype); //创建对象
    prototype.constructor = subType; //增强对象
    subType.prototype = prototype; //指定对象
}
```

用调用 inheritPrototype() 函数的语句，去替换前面例子中为子类型原型赋值的语句。

```js
function SuperType(name){
    this.name = name;
    this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function(){
    alert(this.name);
};
function SubType(name, age){
    SuperType.call(this, name);
    this.age = age;
}
inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function(){
    alert(this.age);
};
```

开发人员普遍认为寄生组合式继承是引用类型最理想的继承范式。

YUI 的 YAHOO.lang.extend() 方法采用了寄生组合继承，从而让这种模式首次
出现在了一个应用非常广泛的 JavaScript 库中。







# 参考资料

[三张图搞懂JavaScript的原型对象与原型链 - 掘金](https://juejin.im/post/5835853f570c35005e413b19)

[【JS基础】Object 对象的原型概念详解 - segmentfault](https://segmentfault.com/a/1190000013017881)

[对原型、原型链、 Function、Object 的理解 - 知乎](https://zhuanlan.zhihu.com/p/22473059)