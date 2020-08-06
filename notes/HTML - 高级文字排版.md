

# 五、高级文字排版

## 引用（Quotation）



### 短引用 `<q>` 

`<q>` 元素定义不需要分段的短的引用（也称行内引用）。浏览器默认将其作为普通文本放入*引号*内表示引用。

```html
<p>WWF 的目标是：<q>构建人与自然和谐共存的世界。</q></p>
```

WWF 的目标是：<q>构建人与自然和谐共存的世界。</q>



### 长引用 `<blockquote>` 

如果一个块级内容从其他地方被引用，应该把它用 `<blockquote>` 元素包裹起来表示，并且在 `cite` 属性里用 URL 来指向引用的资源。

HTML  `<blockquote>` 用于长引用（也称块引用），定义被引用的节。

浏览器通常会对 `<blockquote>` 元素进行缩进处理，作为引用的一个指示符。

```html
<p>以下内容引用自 WWF 的网站：</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>
```

<p>以下内容引用自 WWF 的网站：</p>
<blockquote cite="http://www.worldwildlife.org/who/index.html">
五十年来，WWF 一直致力于保护自然界的未来。
世界领先的环保组织，WWF 工作于 100 个国家，
并得到美国一百二十万会员及全球近五百万会员的支持。
</blockquote>


### 著作标题  `<cite>` 

>  `<cite>` 元素定义*著作的标题*。
>

`<blockquote>` 的 `cite 属性` 内容不会被浏览器显示、不会被屏幕阅读器阅读，需使用 JavaScript 或 CSS，浏览器才会显示。

如果想要确保引用的来源在页面上是可显示的，更好的方法使用 `<cite>` 元素。浏览器通常会以斜体显示 `<cite>` 元素。

```html
<p><cite>The Scream</cite> by Edward Munch. Painted in 1893.</p>
```

<cite>The Scream</cite> by Edward Munch. Painted in 1893.




## 缩略词 `<abbr>` 

HTML `<abbr>` 元素定义缩写或首字母缩略语，并且在 `title` 属性中提供缩写的解释。当光标移动到缩略词上时会出现提示。

对缩写进行标记能够为浏览器、翻译系统以及搜索引擎提供有用的信息。

```html
<p><abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。</p>
```

浏览器显示：<abbr title="World Health Organization">WHO</abbr> 成立于 1948 年。

> **Note**:  `<acronym>` ，基本上与 `<abbr>` 相同，专门用于首字母缩略词而不是缩略语。 然而，它在浏览器的支持中不如 `<abbr>` ，并且具有类似的功能，所以没有意义，已经被废弃了。



## 定义 `<dfn>` 

 `<dfn>` 元素定义项目或缩写的**定义**。项目呈斜体效果，定义在鼠标悬停时会显示或包含在父元素中。

  `<dfn>` 的用法，按照 HTML5 标准中的描述，有点复杂：

1. 如果设置了 `<dfn>` 元素的 title 属性，则定义项目，鼠标悬停时会显示 title 内容。

   ```html
   <p><dfn title="World Health Organization">WHO</dfn> 成立于 1948 年。</p
   ```

   <dfn title="World Health Organization">WHO</dfn> 成立于 1948 年。

2. 如果 `<dfn>` 元素包含具有标题的 `<abbr>` 元素，则 title 定义项目，鼠标悬停时会显示 title 内容。

   ```html
   <p><dfn><abbr title="World Health Organization">WHO</abbr></dfn> 成立于 1948 年。</p>
   ```
   
   <p><dfn><abbr title="World Health Organization">WHO</abbr></dfn> 成立于 1948 年。</p>
   
3. 否则， `<dfn>` 文本内容即是项目，并且父元素包含定义。

   ```html
   <p><dfn>WHO</dfn> World Health Organization 成立于 1948 年。</p>
   ```

   <dfn>WHO</dfn> World Health Organization 成立于 1948 年。

> **注释：**如果希望简而化之，使用第一条，或使用 `<abbr>` 代替。



## 联系信息  `<address>` 

`<address>` 元素定义文档或文章的联系信息（作者/拥有者）。

此元素通常以**斜体**显示。这是块级元素，大多数浏览器会在此元素前后添加折行。

```html
<address>
Written by Donald Duck.<br> 
Visit us at:<br>
Example.com<br>
Box 564, Disneyland<br>
USA
</address>
```

浏览器显示：

*Written by Jon Doe.*
*Visit us at:*
*Example.com*
*Box 564, Disneyland*
*USA*

但要记住的一点是， `<address>` 元素是为了标记编写HTML文档的人的联系方式，而不是任何其他的内容。



## 上标和下标

**`<sup>`** 和 `<sub>` 元素分别定义**上标**和下标，用于日期、化学方程式和数学方程式等。

```html
<p>咖啡因的化学方程式是 C<sub>8</sub>H<sub>10</sub>N<sub>4</sub>O<sub>2</sub>。</p>
<p>如果 x<sup>2</sup> 的值为 9，那么 x 的值必为 3 或 -3。</p>
```

咖啡因的化学方程式是 C<sub>8</sub>H<sub>10</sub>N<sub>4</sub>O<sub>2</sub>。

如果 x<sup>2</sup> 的值为 9，那么 x 的值必为 3 或 -3。



## 双向重写 `<bdo>` 

 `<bdo>` 元素定义双流向覆盖（bi-directional override），用于覆盖当前文本方向。

```html
<bdo dir="rtl">This text will be written from right to left</bdo>
```

如果浏览器支持 bdo，则文本将从右向左进行书写 (rtl，right to left)：

tfel ot thgir morf nettirw eb liw enil sihT



## 计算机代码格式

在显示*计算机代码*示例时，并不需要*可变*的字母尺寸，以及可变的字母间距。

有大量的 HTML 元素可以来标记计算机代码：

- `<code>` ：用于标记计算机通用**代码**。
- **`<pre>`** ：用于**预格式化文本**，用于保留空白字符（通常用于代码块）。

- **`<var>`** ： 用于标记具体**变量**名。
- **`<kbd>`** ：用于标记输入电脑的键盘（或其他类型）输入、**用户输入**。
- `<samp>` ：用于标记计算机程序的输出。



### 键盘输入 `<kbd>` 

 `<kbd>` 元素定义键盘输入：

```html
<p>To open a file, select:</p>
<p><kbd>File | Open...</kbd></p>
```



### 程序输出 `<samp>` 

`<samp>` 元素定义计算机输出示例：

```html
<samp>
demo.example.com login: Apr 12 09:10:17
Linux 2.6.10-grsec+gg3+e+fhs6b+nfs+gr0501+++p3+c4a+gr2b-reslog-v6.189
</samp>
```



### 代码格式 `<code>` 

HTML `<code>` 元素定义编程代码示例：

```html
<code>
var person = { firstName:"Bill", lastName:"Gates", age:50, eyeColor:"blue" }
</code>
```



### 保留空白 `<pre>` 

**`<pre>`** 用于**预格式化文本**。

 `<code>` 元素不保留多余的空格和折行。如需解决该问题，必须在 `<pre>` 元素中包围代码。

```html
<p>Coding Example:</p>
<code>
<pre>
var person = {
    firstName:"Bill",
    lastName:"Gates",
    age:50,
    eyeColor:"blue"
}
</pre>
</code>
```



### 变量格式化 `<var>` 

`<var>` 元素定义数学变量，斜体显示。

```
<var>E = m c<sup>2</sup></var>
```

浏览器显示：<var>E = m c<sup>2</sup></var>



## 时间和日期  `<time>` 

HTML 还支持将时间和日期标记为可供机器识别的格式的 `<time>` 元素。例如：

```html
<time datetime="2016-01-20">2016年1月20日</time>
```

为什么需要这样做？因为世界上有许多种书写日期的格式，上边的日期可能被写成：

- 20 January 2016
- 20th January 2016
- Jan 20 2016
- 20/06/16
- 06/20/16
- The 20th of next month
- 20e Janvier 2016
- 2016年1月20日
- And so on……

不同的格式不容易被电脑识别 — 假如你想自动抓取页面上所有事件的日期并将它们插入到日历中， `<time>` 元素允许附上清晰的、可被机器识别的 时间/日期来实现这种需求。

其他支持的格式，例如：

```html
<!-- 标准简单日期 -->
<time datetime="2016-01-20">20 January 2016</time>
<!-- 只包含年份和月份-->
<time datetime="2016-01">January 2016</time>
<!-- 只包含月份和日期 -->
<time datetime="01-20">20 January</time>
<!-- 只包含时间，小时和分钟数 -->
<time datetime="19:30">19:30</time>
<!-- 还可包含秒和毫秒 -->
<time datetime="19:30:01.856">19:30:01.856</time>
<!-- 日期和时间 -->
<time datetime="2016-01-20T19:30">7.30pm, 20 January 2016</time>
<!-- 含有时区偏移值的日期时间 -->
<time datetime="2016-01-20T19:30+01:00">7.30pm, 20 January 2016 is 8.30pm in France</time>
<!-- 调用特定的周 -->
<time datetime="2016-W04">The fourth week of 2016</time>
```





