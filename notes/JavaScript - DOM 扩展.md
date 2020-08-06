# 二、DOM 扩展

## 1. 选择符 API

Selectors API（www.w3.org/TR/selectors-api/）是由 W3C 发起制定的一个标准，致力于让浏览器原生支持 CSS 查询。

Selectors API Level 1 的核心是两个方法：querySelector() 和 querySelectorAll()。在兼容的浏览器中，可以通过 Document 及 Element 类型的实例调用它们。目前已完全支持Selectors API Level 1的浏览器有 IE 8+、Firefox 3.5+、Safari 3.1+、Chrome 和 Opera 10+。



### 1.1 querySelector()方法

> document.querySelector(*CSS selectors*)

querySelector() 方法接收一个 CSS 选择符，返回与该模式匹配的第一个元素，如果没有找到匹配的元素，返回 null。如果传入了不被支持的选择符，querySelector() 会抛出错误。

通过 Document 类型调用 querySelector() 方法时，会在文档元素的范围内查找匹配的元素。而通过 Element 类型调用 querySelector() 方法时，只会在该元素后代元素的范围内查找匹配的元素。







### 1.2 querySelectorAll() 方法

querySelectorAll() 方法接收一个 CSS 选择符，但返回的是所有匹配的元素而不仅仅是一个元素。这个方法返回的是一个 NodeList 的实例。如果传入了浏览器不支持的选择符或者选择符中有语法错误，querySelectorAll() 会抛出错误。

具体来说，返回的值实际上是带有所有属性和方法的 NodeList，而其底层实现则类似于一组元素的快照，而非不断对文档进行搜索的动态查询。这样实现可以避免使用 NodeList 对象通常会引起的大多数性能问题。

与 querySelector() 类似，能够调用 querySelectorAll() 方法的类型包括 Document、
DocumentFragment 和 Element。

要取得返回的 NodeList 中的每一个元素，可以使用 item() 方法，也可以使用方括号语法。

```js
var i, len, strong;
for (i=0, len=strongs.length; i < len; i++){
    strong = strongs[i]; //或者strongs.item(i)
    strong.className = "important";
}
```





### 1.3 matchesSelector() 方法

Selectors API Level 2 规范为 Element 类型新增了 matchesSelector() 方法。这个方法接收 CSS 选择符，如果调用元素与该选择符匹配，返回 true；否则，返回 false。

```js
if (document.body.matchesSelector("body.page1")){
    //true
}
```

在取得某个元素引用的情况下，使用这个方法能够方便地检测它是否会被 querySelector() 或 querySelectorAll() 方法返回。











## 2. 元素遍历

对于元素间的空格，IE9 及之前版本不会返回文本节点，其他所有浏览器都会返回文本节点。这样，就导致了在使用 childNodes 和 firstChild 等属性时的行为不一致。

为了弥补这一差异，而同时又保持 DOM 规范不变，Element Traversal 规范（www.w3.org/TR/ElementTraversal/）新定义了一组属性。Element Traversal API 为 DOM 元素添加了以下 5 个属性。

- childElementCount：返回子元素（不包括文本节点和注释）的个数。
- firstElementChild：指向第一个子元素；firstChild 的元素版。
- lastElementChild：指向最后一个子元素；lastChild 的元素版。
- previousElementSibling：指向前一个同辈元素；previousSibling 的元素版。
- nextElementSibling：指向后一个同辈元素；nextSibling 的元素版。

支持 Element Traversal 规范的浏览器有 IE 9+、Firefox 3.5+、Safari 4+、Chrome 和Opera 10+。

使用Element Traversal 新增的元素，跨浏览器遍历某元素的所有子元素。

```js
var i,
    len,
    child = element.firstElementChild;
while(child != element.lastElementChild){
    processChild(child); //已知其是元素
    child = child.nextElementSibling;
}
```







## 3. HTML5

### 3.1 与类相关的扩充

为了让开发人员适应并增加对 class 属性的新认识，HTML5 新增了很多 API，致力于简化CSS 类的用法。

#### getElementsByClassName()

> *element*.getElementsByClassName(*classname*)

getElementsByClassName() 方法接收一个参数，即一个包含一或多个类名的字符串，返回文档中所有指定类名的元素集合，作为 NodeList 对象。传入多个类名时，用空格隔开，类名的先后顺序不重要。

支持 getElementsByClassName() 方法的浏览器有 IE 9+、Firefox 3+、Safari 3.1+、Chrome 和 Opera 9.5+。



#### classList 属性

HTML5 新增了一种操作类名的方式，可以让操作更简单也更安全，那就是为所有元素添加 classList 属性。这个classList 属性是新集合类型DOMTokenList 的实例。与其他DOM 集合类似，DOMTokenList 有一个表示自己包含多少元素的length 属性，而要取得每个元素可以使用item()方法，也可以使用方括号语法。此外，这个新类型还定义如下方法。

-  add(value)：将给定的字符串值添加到列表中。如果值已经存在，就不添加了。
-  contains(value)：表示列表中是否存在给定的值，如果存在则返回true，否则返回false。
-  remove(value)：从列表中删除给定的字符串。
-  toggle(value)：如果列表中已经存在给定的值，删除它；如果列表中没有给定的值，添加它。

支持classList 属性的浏览器有Firefox 3.6+和Chrome。





### 3.2 焦点管理



document.hasFocus()



### 3.3 HTMLDocument的变化

#### readyState 属性

支持readyState 属性的浏览器有IE4+、Firefox 3.6+、Safari、Chrome 和Opera 9+。



#### 兼容模式

document.compatMode

后来，陆续实现这个属性的浏览器有Firefox、Safari 3.1+、Opera 和Chrome。最终，HTML5 也把这个属性纳入标准，对其实现做出了明确规定。

#### head 属性

document.head

实现document.head 属性的浏览器包括Chrome 和Safari 5。



### 3.4 字符集属性

#### document.charset

支持document.charset 属性的浏览器有IE 、Firefox 、Safari 、Opera 和Chrome 。

#### document.defaultCharset

支持 document.defaultCharset 属性的浏览器有IE、Safari 和Chrome。





### 3.5 自定义数据属性

HTML5 规定可以为元素添加非标准的属性，但要添加前缀data-，目的是为元素提供与渲染无关的信息，或者提供语义信息。这些属性可以任意添加、随便命名，只要以data-开头即可。









### 3.6 插入标记

#### **innerHTML 属性**





#### **outerHTML 属性**



#### insertAdjacentHTML()





### 3.7 scrollIntoView() 方法





支持scrollIntoView()方法的浏览器有IE、Firefox、Safari 和Opera。



## 4. 专有扩展



### 文档模式

页面的文档模式决定了可以使用什么功能。换句话说，文档模式决定了你可以使用哪个级别的CSS，可以在JavaScript 中使用哪些API，以及如何对待文档类型（doctype）。到了IE9，总共有以下4 种文档模式。











### children属性

### contains()方法

### 插入文本

#### **innerText 属性**





在 body 中添加 DOM 的方法是使用 body.appendChild ( DOM 元素） 。

innerHTML 是指从对象的起始位置到终止位置的全部内容，包括 HTML 标签。

innerText 是指从起始位直到终止位置的内容，但它不包括 HTML 标签。

#### **outerText 属性**



### 滚动

-  scrollIntoViewIfNeeded(alignCenter)：只在当前元素在视口中不可见的情况下，才滚动浏览器窗口或容器元素，最终让它可见。如果当前元素在视口中可见，这个方法什么也不做。如果将可选的alignCenter 参数设置为true，则表示尽量将元素显示在视口中部（垂直方向）。Safari 和Chrome 实现了这个方法。
-  scrollByLines(lineCount)：将元素的内容滚动指定的行高，lineCount 值可以是正值，也可以是负值。Safari 和Chrome 实现了这个方法。
-  scrollByPages(pageCount)：将元素的内容滚动指定的页面高度，具体高度由元素的高度决定。Safari 和Chrome 实现了这个方法。

希望大家要注意的是，scrollIntoView()和scrollIntoViewIfNeeded()的作用对象是元素的
容器，而scrollByLines()和scrollByPages()影响的则是元素自身。
