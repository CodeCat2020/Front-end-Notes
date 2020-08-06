



# 三、样式化文字



## `writing-mode`

CSS 中的书写模式 `writing-mode` 是指文本的排列方向是横向还是纵向的。

`writing-mode` 的三个值分别是：

- `horizontal-tb`：块流向从上至下。对应的文本方向是横向的。
- `vertical-rl`：块流向从右向左。对应的文本方向是纵向的。
- `vertical-lr`：块流向从左向右。对应的文本方向是纵向的。

```css
h1 {  writing-mode: vertical-rl;}
```

```html
<p>Play with writing modes</p>
```

<p style="writing-mode: vertical-rl">Play with writing modes</p>







## CSS 文本



| 属性                | 描述                     |
| :------------------ | :----------------------- |
| **color**           | 设置**文本颜色**         |
| direction           | 设置文本方向。           |
| letter-spacing      | 设置字符间距             |
| line-height         | 设置行高                 |
| text-align          | 对齐元素中的文本         |
| **text-decoration** | 向文本添加修饰           |
| text-indent         | 缩进元素中文本的首行     |
| text-shadow         | 设置文本阴影             |
| **text-transform**  | 控制元素中的字母         |
| unicode-bidi        | 设置或返回文本是否被重写 |
| vertical-align      | 设置元素的垂直对齐       |
| white-space         | 设置元素中空白的处理方式 |
| word-spacing        | 设置字间距               |

注意：没有 text-color 、font-color 属性，文本颜色用 color。



### 文本颜色 color

currentcolor取值为当前元素CSS样式color属性的值

color: currentcolor 和 color: inherit 是等价的





### **行高、字母和单词间距**

```css
p::first-line {
  line-height: 1.5;		/*文本行高设置为字体高度的 1.5 倍*/
  letter-spacing: 2px;	/*字符间距*/
  word-spacing: 4px;	/*字间距*/
}
```



**`line-height` 行高**

**行高是指文本行基线间的垂直距离。** 行距的一半是半行距。行距、font-size 与 line-height 之间的关系如下图所示。

<div align="center"> <img src="pics/前端 - CSS 行高.png" width="500px"/> </div><br>

> https://blog.csdn.net/a2013126370/article/details/82786681









### 文本转换 text-transform

文本转换

- `none`： 防止任何转型。
- `uppercase`： 将所有文本转为大写。
- `lowercase`： 将所有文本转为小写。
- `capitalize`： 转换所有单词让其**首字母大写**。
- `full-width`： 将所有字形转换成全角，即固定宽度的正方形，类似于等宽字体，允许拉丁字符和亚洲语言字形（如中文，日文，韩文）对齐。



### 文本装饰 text-decoration

设置/取消字体上的文本装饰，可用值为：

- **`none`**： 取消已经存在的任何文本装饰。**可以使超链接没有下划线**。
- `underline`： <font style="text-decoration:underline">文本下划线</font>
- `overline`： <font style="text-decoration:overline">文本上划线</font>
- `line-through`： <font style="text-decoration:line-through">穿过文本的线</font>

注意 1：

 `text-decoration` 可以一次接受多个值。

```css
text-decoration: underline overline
```

<font style="text-decoration: underline overline">text-decoration: line-through red wavy</font>

注意 2：

 `text-decoration` 是一个缩写形式，它由 [`text-decoration-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-line), [`text-decoration-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-style) 和 [`text-decoration-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-color) 构成。

```css
text-decoration: line-through red wavy
```

<font style="text-decoration:line-through red wavy">text-decoration: line-through red wavy</font>



### 文字阴影 text-shadow

最多需要 4 个值

```css
text-shadow: 4px 4px 5px red;
```

1. 阴影与原始文本的水平偏移，可以使用大多数的 CSS 单位 [length and size units](https://developer.mozilla.org/zh-CN/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size), 但是 px 是比较合适的。这个值必须指定。
2. 阴影与原始文本的垂直偏移；效果基本上就像水平偏移，除了它向上/向下移动阴影，而不是左/右。这个值必须指定。
3. 模糊半径 - 更高的值意味着阴影分散得更广泛。如果不包含此值，则默认为0，这意味着没有模糊。可以使用大多数的 CSS 单位 [length and size units](https://developer.mozilla.org/zh-CN/Learn/CSS/Introduction_to_CSS/Values_and_units#Length_and_size).
4. 阴影的基础颜色，可以使用大多数的 CSS 颜色单位 [CSS color unit](https://developer.mozilla.org/zh-CN/Learn/CSS/Introduction_to_CSS/Values_and_units#Colors). 如果没有指定，默认为 `black`.



**多种阴影**

可以通过包含以逗号分隔的多个阴影值，将多个阴影应用于同一文本

```css
text-shadow: -1px -1px 1px #aaa,
             0px 4px 1px rgba(0,0,0,0.5),
             4px 4px 5px rgba(0,0,0,0.7),
             0px 0px 7px rgba(0,0,0,0.4);
```



### 文本布局  text-align

对齐

- `left`：左对齐文本。
- `right`：右对齐文本。
- `center`：居中文字
- `justify`：使文本展开，改变单词之间的差距，使所有文本行的宽度相同。你需要仔细使用，它可以看起来很可怕。特别是当应用于其中有很多长单词的段落时。如果你要使用这个，你也应该考虑一起使用别的东西，比如 [`hyphens`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/hyphens)，打破一些更长的词语。



### white-space

如何避免文档流中的空白符合并现象？

空白符合并是标准文档流的特征之一，可以通过设置 white-space 修改这一特征，属性值如下。

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| normal   | 默认。空白会被浏览器忽略。按照文档流特点渲染，合并空白符， 不会渲染换行符，自动换行。 |
| pre      | 空白会被浏览器保留。不会合并空白符，渲染换行符，不会自动换行，相当于`<pre>`元素。 |
| nowrap   | 文本不会换行，文本会在在同一行上继续，直到遇到 `<br>` 标签为止。合并空白符， 不会渲染换行符，不会自动换行。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。不会合并空白符，渲染换行符，自动换行。 |
| pre-line | 合并空白符序列，但是保留换行符。合并空白符，渲染换行符， 自动换行。 |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |





## CSS 字体

| Property                                                     | 描述                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [font](https://www.runoob.com/cssref/pr-font-font.html)      | 在一个声明中设置所有的字体属性       |
| [font-style](https://www.runoob.com/cssref/pr-font-font-style.html) | 指定文本的字体样式                   |
| [font-variant](https://www.runoob.com/cssref/pr-font-font-variant.html) | 以小型大写字体或者正常字体显示文本。 |
| [font-weight](https://www.runoob.com/cssref/pr-font-weight.html) | 指定字体的粗细。                     |
| font-stretch                                                 |                                      |
| font-size                                                    | 指定文本的字体大小                   |
| font-family                                                  | 指定文本的字体系列                   |

`font` 是简写属性，按照以下顺序来写： `font-style`，`font-variant`， `font-weight`，`font-stretch`， `font-size`， `line-height` 和 `font-family`。只有 `font-size` 和 `font-family` 是一定要指定的。

`font-size` 和 `line-height` 属性之间必须放一个正斜杠。

```css
font: italic normal bold normal 3em/1.5 Helvetica, Arial, sans-serif;
```



### 字体种类 font-family

**网页安全字体**

可以应用到所有系统

| 字体名称        | 泛型       | 注意                                                         |
| :-------------- | :--------- | :----------------------------------------------------------- |
| Arial           | sans-serif | 通常认为最佳做法还是添加 Helvetica 作为 Arial 的首选替代品，尽管它们的字体面几乎相同，但 Helvetica 被认为具有更好的形状，即使 Arial 更广泛地可用。 |
| Courier New     | monospace  | 替代版本 Courie，首选替代方案。                              |
| Georgia         | serif      |                                                              |
| Times New Roman | serif      | 替代版本 Times，首选替代方案。                               |
| Trebuchet MS    | sans-serif | 应该小心使用这种字体——它在移动操作系统上并不广泛。           |
| Verdana         | sans-serif |                                                              |



在 CSS 中，有两种不同类型的字体系列名称：

- 通用字体系列 - 拥有相似外观的字体系统组合
- 特定字体系列 - 具体的字体系列（比如 "Times" 或 "Courier"）

CSS 定义了 5 种通用字体系列：

| 名称         | 定义                                                         |
| :----------- | :----------------------------------------------------------- |
| `serif`      | 有衬线的字体 （衬线一词是指字体笔画尾端的小装饰，存在于某些印刷体字体中） |
| `sans-serif` | 没有衬线的字体。                                             |
| `monospace`  | 每个字符具有相同宽度的字体，通常用于代码列表。               |
| `cursive`    | 用于模拟笔迹的字体，具有流动的连接笔画。                     |
| `fantasy`    | 用来装饰的字体                                               |



**字体栈**

无法保证网页上使用的字体的可用性，可以提供一个**字体栈**，这样的话，浏览器就有多种字体可以选择了。

只需包含一个`font-family` 属性，其值由几个用逗号分离的字体名称组成。

```css
p {
  font-family: "Trebuchet MS", Verdana, sans-serif;
}
```

在字体栈的最后提供一个合适的通用的字体名称是个不错的办法。

如果没有其他选项可用，那么段落将被赋予浏览器的默认衬线字体 - 通常是Time New Roman - 这对于 sans-serif 字体是不利的！

> **注意**：有一些字体名称不止一个单词，比如 `Trebuchet MS` ，那么就需要用引号包裹。



### 风格和粗细

**font-style**

该属性有三个值：

- normal - 文本正常显示
- italic - 文本斜体显示
- oblique - 文本倾斜显示

**italic 和 oblique 的区别**

font-style 非常简单：用于在 normal 文本、italic 文本和 oblique 文本之间选择。唯一有点复杂的是明确 italic 文本和 oblique 文本之间的差别。

斜体（italic）是一种简单的字体风格，对每个字母的结构有一些小改动，来反映变化的外观。与此不同，倾斜（oblique）文本则是正常竖直文本的一个倾斜版本。

通常情况下，italic 和 oblique 文本在 web 浏览器中看上去完全一样。



**font-weight**

设置文字的粗体大小。lighter（细体），bolder，normal（正常），bold（加粗），extrabold, -black

很少会用到 normal 和 bold 以外的值：

- normal, bold: 普通或者加粗的字体粗细
- lighter, bolder: 将当前元素的粗体设置为比其父元素粗体更细或更粗一步。100–900: 数值粗体值，如果需要，可提供比上述关键字更精细的粒度控制。

注意：没有 text-size 属性。











### 字体变形 font-variant









## CSS 链接

链接的状态：

- a:link - 正常，未访问过
- a:visited - 已访问过
- a:hover - 当用户鼠标放在链接上时
- a:active - 链接被点击的那一刻
- a:focus - 被选中的时候 （比如通过键盘的 Tab 移动到这个链接的时候，或者使用编程的方法来选中这个链接 [`HTMLElement.focus()`](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/focus)） 

当设置为若干链路状态的样式，也有一些顺序规则：

- a:hover 必须跟在 a:link 和 a:visited 后面
- a:active 必须跟在 a:hover 后面





## CSS 列表

| 属性                                                         | 描述                                               |
| :----------------------------------------------------------- | :------------------------------------------------- |
| [list-style](https://www.runoob.com/cssref/pr-list-style.html) | 简写属性。用于把所有用于列表的属性设置于一个声明中 |
| [list-style-image](https://www.runoob.com/cssref/pr-list-style-image.html) | 将图像设置为列表项标志。                           |
| [list-style-position](https://www.runoob.com/cssref/pr-list-style-position.html) | 设置列表中列表项标志的位置。                       |
| [list-style-type](https://www.runoob.com/cssref/pr-list-style-type.html) | 设置列表项标志的类型。                             |
| marker-offset                                                |                                                    |

**list-style 速记属性**

可以用一个单独的速记属性 [`list-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style) 来设置。

```css
ul {
  list-style-type: square;
  list-style-image: url(example.png);
  list-style-position: inside;
}
```

可以被如下方式代替：

```css
ul {  list-style: square url(example.png) inside;}
```

属性值可以任意顺序排列，可以设置一个，两个或者三个值（该属性的默认值为 disc, none, outside），如果指定了 type 和 image，如果由于某种原因导致图像无法加载，则 type 将用作回退。



 **list-style-type**

 `list-style-type` 属性允许设置项目符号点的类型。

- square：带有正方形项目的列表

```css
ol {
  list-style-type: upper-roman;
}
```

通过 `list-style-type` [参考页面](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style-type)查找到更多选项。






