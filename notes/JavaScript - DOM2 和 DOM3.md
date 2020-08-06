

# 三、DOM2 和 DOM3

DOM1 级主要定义的是HTML 和XML 文档的底层结构。DOM2 和DOM3 级则在这个结构的基础上引入了更多的交互能力，也支持了更高级的XML 特性。





## 1. DOM 变化



## 2. 样式

在 HTML 中定义样式的方式有 3 种： `<link/>` 元素； `<style/>` 元素； `style` 特性。“DOM2 级样式”模块围绕这 3 种应用样式的机制提供了一套 API。

要确定浏览器是否支持 DOM2 级定义的 CSS 能力，可以使用下列代码。

```js
var supportsDOM2CSS = document.implementation.hasFeature("CSS", "2.0");
var supportsDOM2CSS2 = document.implementation.hasFeature("CSS2", "2.0");
```





### 2.1 访问元素的样式

任何支持 style 特性的 HTML 元素在 JavaScript 中都有一个对应的 style 属性。

这个 style 对象是 CSSStyleDeclaration 的实例，包含着通过 HTML 的 style 特性指定的所有样式信息，但不包含与外部样式表或嵌入样式表经层叠而来的样式。

对于使用短划线的 CSS 属性名，必须将其转换成驼峰大小写形式，才能通过 JavaScript 来访问。

下表列出了几个常见的 CSS 属性及其在 style 对象中对应的属性名。

| CSS 属性         | JavaScript 属性       |
| ---------------- | --------------------- |
| background-image | style.backgroundImage |
| color            | style.color           |
| display          | style.display         |
| font-family      | style.fontFamily      |

多数情况下，都可以通过简单地转换属性名的格式来实现转换。但有些元素不能，比如 float。由于 float 是JavaScript 中的保留字，因此不能用作属性名。“DOM2 级样式”规范规定样式对象上相应的属性名应该是cssFloat；Firefox、Safari、Opera 和Chrome 都支持这个属性，而 IE 支持的则是 styleFloat。

在标准模式下，所有度量值都必须指定一个度量单位。在混杂模式下，可以将 style.width 设置为"20"，浏览器会假设它是"20px"。在实践中，最好始终都指定度量单位。

#### DOM 样式属性和方法

#### 计算的样式









### 2.2 操作样式表



CSSStyleSheet 类型表示的是样式表

#### CSS 规则

#### 创建规则

#### 删除规则



### 2.3 元素大小

#### 偏移量

下列4 个属性可以取得元素的偏移量。

-  offsetHeight：元素在垂直方向上占用的空间大小，以像素计。包括元素的高度、（可见的）水平滚动条的高度、上边框高度和下边框高度。
-  offsetWidth：元素在水平方向上占用的空间大小，以像素计。包括元素的宽度、（可见的）垂直滚动条的宽度、左边框宽度和右边框宽度。
-  offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离。
-  offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离。

#### 客户区大小

- clientWidth
- clientHeight



#### 滚动大小

以下是4 个与滚动大小相关的属性。

-  scrollHeight：在没有滚动条的情况下，元素内容的总高度。
-  scrollWidth：在没有滚动条的情况下，元素内容的总宽度。
-  scrollLeft：被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。
-  scrollTop：被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。



#### 确定元素的大小



## 3. 遍历

### 3.1 NodeIterator

### 3.2 TreeWalker



## 4. 范围

### 4.1 DOM 中的范围

createRange()

#### 用DOM 范围实现简单选择

#### 用DOM 范围实现复杂选择

#### 操作DOM 范围中的内容

#### 插入DOM 范围中的内容

#### 折叠DOM 范围

#### 比较DOM 范围

#### 复制DOM 范围

#### 清理DOM 范围







### 4.2 IE8 及更早版本中的范围

#### 用IE 范围实现简单的选择



#### 使用IE 范围实现复杂的选择

#### 操作IE 范围中的内容

#### 折叠IE 范围

#### 比较IE 范围

#### 复制IE 范围



