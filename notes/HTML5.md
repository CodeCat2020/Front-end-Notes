

# 一、语义

## HTML5 定义

**什么是 HTML 5?**

HTML5 是最新的第五代 HTML 标准。HTML5 的设计目的是为了在移动设备上支持多媒体。不仅提供丰富的媒体支持，而且还增强了对创建一个能够与用户进行交互的 Web 应用的支持，使本地数据和服务器交互比以前更有效，更容易。

HTML5 仍处于完善之中。然而，大部分现代浏览器已经具备了某些 HTML5 支持。



**HTML5 是如何起步的？**

HTML5 是 W3C 与 WHATWG 合作的结果。

WHATWG 致力于 web 表单和应用程序，而 W3C 专注于 XHTML 2.0。在 2006 年，双方决定进行合作，来创建一个新版本的 HTML。

HTML5 草案的前身名为 Web Applications 1.0。于 2004 年被 WHATWG 提出，于 2007 年被 W3C 接纳，并成立了新的 HTML 工作团队。在 2008 年1 月22 日，第一份正式草案已公布，预计将在 2010 年 9 月正式向公众推荐。WHATWG 表示该规范是目前正在进行的工作，仍须多年的努力。



HTML5 的优点与缺点？

优点： 

- a、网络标准统一、HTML5 本身是由 W3C 推荐出来的。
- b、多设备、跨平台 
- c、即时更新。
- d、提高可用性和改进用户的友好体验；
- e、有几个新的标签，这将有助于开发人员定义重要的内容； 
- f、可以给站点带来更多的多媒体元素(视频和音频)；  
- g、可以很好的替代Flash和Silverlight；
- h、涉及到网站的抓取和索引的时候，对于 SEO 很友好； 
- i、被大量应用于移动应用程序和游戏。 

缺点： 

- 安全：像之前Firefox4的web socket和透明代理的实现存在严重的安全问题，同时web storage、web socket 这样的功能很容易被黑客利用，来盗取用户的信息和资料。 
- 完善性：许多特性各浏览器的支持程度也不一样。 
- 技术门槛：HTML5简化开发者工作的同时代表了有许多新的属性和API需要开发者学习，像web worker、web socket、web storage 等新特性，后台甚至浏览器原理的知识，机遇的同时也是巨大的挑战 
- 性能：某些平台上的引擎问题导致HTML5性能低下。 
- 浏览器兼容性：最大缺点，IE9 以下浏览器几乎全军覆没。



HTML5 标签的作用（用途）？

- 本地数据存储
- 访问本地文件
- 本地 SQL 数据
- 缓存引用
- Javascript 工作者
- XHTMLHttpRequest 2





## DOCTYPE 声明

用 DOCTYPE 声明新增的结构元素和功能元素来区别 HTML 和 HTML5。

```html
<!DOCTYPE html>
```

这样做会让目前还不支持 HTML5 的浏览器采用严格模式解析，意味着他们会解析 HTML5 中兼容的旧的 HTML 的标签的部分，而忽略他们不支持的 HTML5 的新特性。

HTML5 doctype 比以前更短，更简单，更容易被记住并且减少必须下载的字节数。

```html
<meta charset="UTF-8">
```





## 浏览器支持

最新版本的 Safari、Chrome、Firefox 以及 Opera 支持某些 HTML5 特性。IE 9 将支持某些 HTML5 特性。

IE9 以下版本浏览器兼容 HTML5 的方法，使用本站的静态资源的html5shiv包：

```
<!--[if lt IE 9]>    <script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js"></script> <![endif]-->
```

载入后，初始化新标签的CSS：

```
/*html5*/ article,aside,dialog,footer,header,section,nav,figure,menu{display:block}
```

如何处理HTML5 新标签的浏览器兼容问题？

IE8, IE7 、IE6 支持用document.createElement 产生标签，可以利用这一特性让这些浏览器支持HTMLS 新标签。浏览器支持新标签后，还需要添加标签默认的样式（最好的方式是直接使用成熟的框架， 使用最多的是htm ! Sshim 框架） ， 可以用IE hack 引入该框架。





## 新增元素




HTML5 添加了很多语义元素。



**脚本元素**

- template ：通过 JavaScript 在运行时实例化内容的容器。

### **章节元素**



以构建更好的文档结构：

| 标签        | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| `<article>` | 定义文档内的文章。                                           |
| `<aside>`   | 定义页面内容之外的内容。用于表达注记、贴士、侧栏、摘要、插入的引用等作为补充主体的内容。 |
| `<footer>`  | 定义 section 或 document、page 的页脚。通常会标出网站的相关信息。 |
| `<header>`  | 定义section 或 document、page 的页眉。                       |
| main        | 定义文档的主内容。定义文档中主要或重要的内容。               |
| `<nav>`     | 定义文档内的导航链接。navigator 的缩写。                     |
| `<section>` | 定义文档中的节。                                             |



`<section>`

```html
<section>
  <h1>Heading</h1>
  <p>Bunch of awesome content</p>
</section>
```



### **组织内容**

- `<figure>`：定义媒介内容的分组，以及它们的标题。定义自包含内容，比如图示、图表、照片、代码清单等等。

- `<figcaption>`  ：定义 `<figure>` 元素的标题。  

- `hgroup` ：用来对标题元素进行分组。将多个 `<h1>` 至 `<h6>` 的子元素组装到一起。

  ```html
  <hgroup>
  <h1>Welcome to my WWF</h1>
  <h2>For a living planet</h2>
  </hgroup>
  ```

  



### **文字形式**

| 标签       | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| `<bdi>`    | 定义与其他文本不同的文本方向。                               |
| data       | 关联一个内容的*机器可读的等价形式* （该元素只在 WHATWG 版本的 HTML 标准中，不在 W3C 版本的 HTML5 标准中）。 |
| **`mark`** | 定义有记号的文本。定义重要或强调的内容。**高亮显示，不会加粗**。 |
| `<rp>`     | 定义若浏览器不支持 ruby 元素显示的内容。                     |
| `<rt>`     | 定义 ruby 注释的解释。定义关于字符的解释/发音（用于东亚字体）。 |
| `<ruby>`   | 定义 ruby 注释（用于东亚字体）。                             |
| `<time>`   | 定义日期/时间。                                              |
| `<wbr>`    | 建议换行 (Word Break Opportunity)，定义可能的折行（line-break）。 |



### **表单元素**



| 标签           | 描述                                                       |
| :------------- | :--------------------------------------------------------- |
| **`datalist`** | 定义下拉列表。定义输入控件的预定义选项。                   |
| `keygen`       | 定义生成密钥。定义键对生成器字段（用于表单）。             |
| **`output`**   | 定义输出的一些类型。定义计算结果。                         |
| `<progress>`   | 定义任务进度。                                             |
| `<meter>`      | 定义预定义范围内的度量。定义已知范围（尺度）内的标量测量。 |



**HTML5 `<datalist>` 元素**

`<datalist>` 元素规定输入域的选项列表。使用 `<input>` 元素的列表属性与 `<datalist>` 元素绑定。

```html
<input list="browsers">
 
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
```



**HTML5 `<keygen>` 元素**

`<keygen>` 标签规定用于表单的密钥对生成器字段，提供一种验证用户的可靠方法。

当提交表单时，会生成两个键，一个是私钥，一个公钥。私钥存储于客户端，公钥则被发送到服务器。公钥可用于之后验证用户的客户端证书。

带有 keygen 字段的表单：

```html
<form action="demo_keygen.asp" method="get">
用户名: <input type="text" name="usr_name">
加密: <keygen name="security">
<input type="submit">
</form>
```



**HTML5 `<output>` 元素**

 `<output>` 元素用于不同类型的输出，比如计算或脚本输出：

```html
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
<input type="range" id="a" value="50">100 +
<input type="number" id="b" value="50">=
<output name="x" for="a b"></output>
</form>
```



**HTML5 `<progress>` 元素**

`<progress>` 定义运行中的任务进度（进程）。

| 属性                                                         | 值       | 描述               |
| :----------------------------------------------------------- | :------- | :----------------- |
| [max](https://www.runoob.com/tags/att-progress-max.html)**New** | *number* | 规定需要完成的值。 |
| [value](https://www.runoob.com/tags/att-progress-value.html)**New** | *number* | 规定进程的当前值。 |

用法：

```html
<progress value="23" max="100"></progress>
```

<progress value="23" max="100"></progress>

两属性的值为空，或 value 为空而 max 不为空时，显示效果一样。

```html
<progress value="" max=""></progress>
```

<progress value="" max="">
</progress>

不填写 max 和 value 会自动滑动。


```html
<progress></progress>	<!--自动来回滑动-->
```

<progress></progress>





### **嵌入内容**

| 音频/视频标签 | 描述                                             |
| :------------ | :----------------------------------------------- |
| `<audio>`     | 定义声音或音乐内容。                             |
| `<embed>`     | 定义外部应用程序的容器（比如插件）。             |
| `<source>`    | 定义媒介源。定义 `<video>` 和 `<audio>` 的来源。 |
| `<track>`     | 定义 `<video>` 和 `<audio>`的轨道。              |
| `<video>`     | 定义视频或影片内容。                             |
| **图像标签**  |                                                  |
| `<canvas>`    | 定义使用 JavaScript 的图像绘制。                 |
| svg           | 定义使用 SVG 的图像绘制。                        |
| **数学公式**  |                                                  |
| math          | 定义一段*数学公式* 。                            |

使用 [CSS3 2D 转换](https://www.runoob.com/css3/css3-2dtransforms.html)、[CSS3 3D 转换](https://www.runoob.com/css3/css3-3dtransforms.html)。



**HTML5 MathML**

MathML 是数学标记语言，是一种基于 XML 的标准，用来在互联网上书写数学符号和公式的置标语言。

HTML5 可以在文档中使用 MathML 元素，对应的标签是 `<math>` `</math>` 。

```html
<math xmlns="http://www.w3.org/1998/Math/MathML">
    <mrow>
        <msup><mi>a</mi><mn>2</mn></msup>
        <mo>+</mo>
        <msup><mi>b</mi><mn>2</mn></msup>
        <mo>=</mo>
        <msup><mi>c</mi><mn>2</mn></msup>
    </mrow>
</math>
```



### **交互元素**

| 元素        | 描述                                             |
| :---------- | :----------------------------------------------- |
| `<details>` | 定义元素的细节。定义用户可查看或隐藏的额外细节。 |
| summary     | 定义 `<details>` 元素的可见标题。                |
| menuitem    | 定义用户能够从弹出菜单调用的命令/菜单项目。      |
| `<memu>`    | 代表菜单。                                       |

其它：

-  `<command>` 定义命令按钮。只有 IE 9 支持 `<command>` 标签，其他之前版本或者之后版本的 IE 浏览器不支持 `<command>` 标签。

-  dialog  定义对话框或窗口。该元素包含 dt 和 dd 这两个组合元素， dt 用于表示说话者，而 dd 用来表示说话内容。




 `<memu>` 标签定义了一个命令列表或菜单。

目前主流浏览器并不支持 `<memu>` 标签。HTML 4.01的 `<memu>` 元素已废弃。HTML5 中 `<memu>` 元素已被重新定义。











## 新增属性

HTML5 中可以使用 data-* 自定义属性



### 表单属性

**新表单控件**

`<input>` 的 type 的新属性值：color、date、datetime、datetime-local、month、week、time、email、number、range、search、tel 和 url。



HTML5 的 `<form>` 和 `<input>` 标签添加了几个新属性。

 `<form>` 新属性：

- autocomplete：规定 form 应该拥有自动完成功能。
- novalidate：布尔属性，规定在提交表单时不应该验证 form 或 input 域。

 `<input>` 新属性：

- autocomplete：规定 input 域应该拥有自动完成功能。
- autofocus：布尔属性，规定在页面加载时，域自动地获得焦点。
- form：规定输入域所属的一个或多个表单。引用一个以上的表单，使用空格分隔。
- formaction：用于描述表单提交的 URL 地址，覆盖 `<form>` 元素中的action 属性。
- formenctype：描述了表单提交到服务器的数据编码，覆盖 `<form>` 元素的 enctype 属性。
- formmethod
- formnovalidate
- formtarget
- height 与 width
- list
- min 与 max
- **multiple**：布尔属性，规定 `<input>` 元素中可选择多个值。
- **pattern** (regexp)：描述了一个正则表达式用于验证 `<input>` 元素的值。适用于以下类型的type ：text，search，url，tel，email 和 password。
- **placeholder**
- **required**：布尔属性，规定必须在提交之前填写输入域（不能为空）。
- step：为输入域规定合法的数字间隔。



**`autocomplete` 属性**

autocomplete 属性规定 form 或 input 域应该拥有自动完成功能。

当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项。

autocomplete 属性有可能在 form元素中是开启的，而在 input元素中是关闭的。

autocomplete 适用于 `<form>` 标签，以及具有以下 type 属性值的 `<input>` 标签：text, search, url, telephone, email, password, datepickers, range 以及 color。

**提示：**某些浏览器中，可能需要启用自动完成功能，以使该属性生效。



将不想要提示的 form 元素下的 input 元素的 autocomplete 属性设置为 off。

```html
<form action="demo-form.php" autocomplete="on">
  First name:<input type="text" name="fname"><br>
  Last name: <input type="text" name="lname"><br>
  E-mail: <input type="email" name="email" autocomplete="off"><br>
  <input type="submit">
</form>
```











## 已移除元素

HTML5 废弃了哪些 HTML4 标签？

纯表现的元素，包括 basefont 、big 、center 、font 、strike 、tt 等。对可用性产生负面影响的元素，包括 frame 、frameset 、noframes 等。



HTML5 中不再支持下面哪个元素？哪些是合法的 HTML5 标签？

| 标签            | 描述                                                    |
| --------------- | ------------------------------------------------------- |
| `<acronym>`     | 定义只取首字母的缩写。（不支持 HTML5）                  |
| `<applet>`      | 定义嵌入的 applet。（不支持 HTML5）                     |
| `<basefont>`    | 定义页面中文本的默认字体、颜色或尺寸。（不支持 HTML5）  |
| `<big>`         | 使字体加大一号。（不支持 HTML5）                        |
| **`<center>`**  | 定义居中文本。（不支持 HTML5）                          |
| `<dir>`         | 定义目录列表。（不支持 HTML5）                          |
| **`<font>`**    | 定义文字的字体、尺寸和颜色。（不支持 HTML5）            |
| `<frame>`       | （不支持 HTML5）                                        |
| `<frameset>`    | 用于包含 `<frame>` 的 HTML 元素。（不支持 HTML5）       |
| **`<marquee>`** | 插入一段**滚动**的文字。                                |
| `<noframes>`    | （不支持 HTML5）                                        |
| `<listing>`     | 定义加删除线文本。（不支持 HTML5）                      |
| `<strike>`      | 定义加删除线文本。用 `<del>` 代替。（HTML 4.01 已废弃） |
| `<tt>`          | 定义打字机文本。（不支持 HTML5）                        |





## 新的 API

- Media API
- Text Track API
- Application Cache API
- User Interaction
- Data Transfer API
- Command API
- Constraint Validation API
- History API

















