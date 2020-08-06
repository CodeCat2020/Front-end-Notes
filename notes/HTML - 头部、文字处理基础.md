# 二、HTML 头部

**什么是 HTML 头部？**

HTML 头部是包含在 `<head>` 元素里面的内容。`<head>` 元素是所有头部元素的容器。

`<head>` 里面的内容不会在浏览器中显示，作用是包含一些页面的[元数据](https://developer.mozilla.org/zh-CN/docs/Glossary/Metadata)（Metadata）。元数据，就是描述数据的数据。

```html
<head>
  <meta charset="utf-8">
  <title>My test page</title>
</head>
```

以下标签都可以添加到 head 部分：`<tilte>`、 `<base>` 、 `<link>` 、 `<meta>` 、`<script>` 、`<noscript>` 以及 `<style>` 。



##  `<tilte>` 元素

 `<tilte>` 标签定义文档的标题，**在所有 HTML/XHTML 文档中都是<span style="color:red">必需</span>的**。

- 定义浏览器工具栏中的标题
- 页面被添加到收藏夹时显示的标题。浏览器收藏网页时， `<tilte>` 的内容被作为建议的书签名。
- 显示在搜索引擎结果中的页面标题。 `<tilte>` 的内容也被用在搜索的结果中。





##  `<base>` 元素

 `<base>` 标签为页面上的所有链接规定默认地址或默认目标（target）：

```html
<head>
	<base href="http://www.w3school.com.cn/images/" />
	<base target="_blank" />
</head>
```



##  `<link>` 元素

 `<link>` 标签定义文档与外部资源之间的关系，最常用于连接样式表。

- `rel="stylesheet"` 属性表明这是文档的样式表
- `href` 包含了样式表文件的路径

```html
<head>
	<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```



##  `<style>` 元素

 `<style>` 标签用于为 HTML 文档定义样式信息。

也可以在 `<style>` 元素内规定 HTML 元素在浏览器中呈现的样式：

```html
<head>
	<style type="text/css">
		body {background-color:yellow}
		p {color:blue}
	</style>
</head>
```



##  `<meta>` 元素

`<meta>` 标签提供关于 HTML 文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。

 `<meta>` 元素属性：

- `charset` 指定文档中字符的编码；

- `name` 和 `content` 属性的作用是描述页面的内容。
  - `name` 指定了 `<meta>` 元素的类型； 说明该元素包含了什么类型的信息。
  - `content` 指定了实际的元数据内容。



### charset 属性

**字符编码**

中文编码：在头部将字符声明为 UTF-8 或 GBK。

```html
<meta charset="utf-8">
```

> **注**：一些浏览器（比如 Chrome ）会自动修正错误的编码。为了避免在其他浏览器中可能出现的潜在问题，无论如何，你仍然应该为你的页面手动设置编码为 `utf-8`





### name 和 content 属性



**添加作者和描述**

```html
<meta name="author" content="Chris Mills">
```



**针对搜索引擎的关键词**

description 也被使用在搜索引擎显示的结果页中。它可能或让你的页面在搜索引擎的相关的搜索出现得更多 （Search Engine Optimization，SEO，搜索引擎优化）

下面的 meta 元素定义页面的描述：

```html
<meta name="description" content="The MDN Learning Area aims to provide
complete beginners to the Web with all they need to know to get
started with developing web sites and applications.">
```

```html
<meta name="description" content="Free Web tutorials on HTML, CSS, XML" />
```

下面的 meta 元素定义页面的关键词：

```html
<meta name="keywords" content="HTML, CSS, XML" />
```

> **Note**：许多 `<meta>` 特性已经不再使用。 例如， `name="keywords"` （提供关键词给搜索引擎，根据不同的搜索词，查找到相关的网站）——已经被搜索引擎忽略了， 因为作弊者填充了大量关键词到keyword， 错误地引导搜索结果。



**其他类型的元数据**

例如，Facebook 编写的元数据协议 [Open Graph Data](http://ogp.me/) 为网站提供了更丰富的元数据。在 MDN 源代码中，你会发现：

```html
<meta property="og:image" content="https://developer.cdn.mozilla.net/static/img/opengraph-logo.dc4e08e2f6af.png">
<meta property="og:description" content="The Mozilla Developer Network (MDN) provides
information about Open Web technologies including HTML, CSS, and APIs for both Web sites
and HTML5 Apps. It also documents Mozilla products, like Firefox OS.">
<meta property="og:title" content="Mozilla Developer Network">
```

上面代码展现的一个效果：当你在 Facebook 上链接到 MDN 时，该链接将显示一个图像和描述，这为用户提供更丰富的体验。

<div align="center"> <img src="https://mdn.mozillademos.org/files/12349/facebook-output.png" width=300px /> </div><br>

Twitter 还拥有自己的类型的专有元数据协议，当网站的 URL 显示在 twitter.com 上时，它具有相似的效果。例如下面：

```html
<meta name="twitter:title" content="Mozilla Developer Network">
```







##  `<script>` 元素

 `<script> ` 标签用于定义客户端脚本，比如 JavaScript。`<script> ` 不是空元素，因此需要一个结束标记。

```html
<script src="my-js-file.js"></script>
```

除了指向外部脚本文件，还可以选择将脚本放入 `<script> ` 元素中。

 `<script> ` 放在文档的尾部（ `</body>` 标签之前）更好，可以确保在加载脚本之前浏览器已经解析了 HTML 内容（如果脚本加载某个不存在的元素，浏览器会报错）。





## `<noscript>` 元素

`<noscript>` 标签提供无法使用脚本时的替代内容，比如：浏览器禁用脚本，或浏览器不支持客户端脚本。

`<noscript>` 元素可包含普通 HTML 页面的 body 元素中能够找到的所有元素。

只有在浏览器无法使用脚本时，才会显示 `<noscript>` 元素中的内容：

```html
<script>
	document.write("Hello World!")
</script>
<noscript>抱歉，你的浏览器不支持 JavaScript!</noscrip
```





## 自定义图标

现代浏览器在各种场合使用 favicons（Favorites Icon，网站头像），如打开的页面标签页和书签面板中的书签页面。

16 x 16 像素是这种图标的第一种类型。

页面添加图标：

1. 将其保存在与网站的索引页面相同的目录中，以 .ico 格式保存。

   大多数浏览器支持更通用的格式，如 .gif 或 .png，但使用 ICO 格式可以确保图标能在如 IE 6 一样久远的浏览器中显示。

2. 添加到HTML `<head>` 中引用它：

   ```html
   <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
   ```

还有很多其他的图标类型可以考虑。 例如， MDN 主页的源代码：

```html
<!-- third-generation iPad with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="https://developer.cdn.mozilla.net/static/img/favicon144.a6e4162070f4.png">
<!-- iPhone with high-resolution Retina display: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="https://developer.cdn.mozilla.net/static/img/favicon114.0e9fabd44f85.png">
<!-- first- and second-generation iPad: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="https://developer.cdn.mozilla.net/static/img/favicon72.8ff9d87c82a0.png">
<!-- non-Retina iPhone, iPod Touch, and Android 2.1+ devices: -->
<link rel="apple-touch-icon-precomposed" href="https://developer.cdn.mozilla.net/static/img/favicon57.a2490b9a2d76.png">
<!-- basic favicon -->
<link rel="shortcut icon" href="https://developer.cdn.mozilla.net/static/img/favicon32.e02854fdcf73.png">
```

这些元素提供高分辨率图标，当网站保存到 iPad 的主屏幕时使用。

> **注**：如果你的网站使用了内容安全策略（Content Security Policy, CSP）来增加安全性，这个策略会应用在图标上。如果你遇到了图标没有被加载的问题，你需要确认认 [`Content-Security-Policy`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy) header的 [`img-src` directive](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/img-src) 没有禁止访问图标。



## 为文档设定主语言

通过添加 lang 属性到开始标签 `<html>` 中来实现：

```html
<html lang="en-US">
```

用途：

- HTML 文档会被搜索引擎更有效地索引。例如，允许它在特定于语言的结果中正确显示。
- 对于使用屏幕阅读器的视障人士很有用。比如， 法语和英语中都有“six”这个单词，但是发音却完全不同。

还可以将文档的分段设置为不同的语言。

```html
<p>Japanese example: <span lang="jp">ご飯が熱い。</span>.</p>
```

更多详情：[Language tags in HTML and XML](https://www.w3.org/International/articles/language-tags/)



# 三、HTML 文字处理基础

大部分的文本结构由标题和段落组成。

## HTML 标题

标题（Heading）是通过 `<h1>` -  `<h6>`  等标签进行定义的。这些元素都是块级元素。

`<h1>` 定义最大的标题。 `<h6>` 定义最小的标题。`<h1>` 表示主标题（the main heading），`<h2>` 表示二级子标题（subheadings），`<h3>` 表示三级子标题（sub-subheadings），等等。

```html
<h4>This is a heading</h4>
<h6>This is a heading</h6>
```

<h4>This is a heading</h4>
<h6>This is a heading</h6>



最佳实践：

- 只对每个页面使用一次 `<h1>`。
- 请确保在层次结构中以正确的顺序使用标题。不要使用 `<h3>` 来表示副标题， `<h2>` 来表示副副标题。
- 在可用的六个标题级别中，每页使用不超过三个，除非有必要。较深的标题层次结构难以操作且难以导航。如果可能，建议将内容分散在多个页面上。

标题很重要

- 确保将 heading 标签只用于标题。不要仅仅是为了产生粗体或大号的文本而使用标题。

- 搜索引擎使用标题为网页的结构和内容编制索引。

- 用户可以通过标题来快速浏览网页，用标题呈现文档结构很重要。




## HTML 段落

**可以把 HTML 文档分割为若干段落。**

段落是通过 `<p>` 标签定义的。 `<p>` 是块级元素。

```html
<p>我是一个段落，千真万确。</p>
```

> **提示：**使用空的段落标记 `<p>`  `</p>` 去插入一个空行是个坏习惯。用 `<br />`  标签代替它！（但是不要用 `<br />`   标签去创建列表。）



## HTML 列表

HTML 支持有序、无序和定义列表。

列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。

### 无序列表

无序列表始于 ` <ul> ` 标签。每个列表项始于 ` <li> ` 。使用粗体圆点（小黑圆圈）进行标记。

```html
<ul>
	<li>Coffee</li>
	<li>Milk</li>
</ul>
```

浏览器显示如下：

- Coffee
- Milk



### 有序列表

有序列表始于 `<ol>` 标签。每个列表项始于 `<li>` 标签。使用数字进行标记。

```html
<ol>
	<li>Coffee</li>
	<li>Milk</li>
</ol>
```

浏览器显示如下：

1. Coffee
2. Milk



### 定义列表

定义列表不仅仅是一列项目，而是项目及其注释的组合。也称为描述列表（description list）。

这种列表的目的是标记一组项目及其相关描述，例如术语和定义，或者是问题和答案等。

列表以 `<dl>` 标签开始。每个列表项以 `<dt>` 开始。每个列表项的定义以 `<dd>` 开始。

浏览器的默认样式会在**描述列表的描述部分**（description description）和**描述术语**（description terms）之间产生缩进。

```html
<dl>
	<dt>Coffee</dt>				<!--dt 和 dd 并列-->
	<dd>Black hot drink</dd>
	<dt>Milk</dt>
	<dd>White cold drink</dd>
</dl>
```

浏览器显示如下：

- Coffee

  Black hot drink

- Milk

  White cold drink



### 嵌套列表

将一个列表嵌入到另一个列表，叫做嵌套列表（Nesting lists）。嵌套时，子列表与 li 并列。

```html
<ol>
  <li>步骤1</li>
  <li>步骤2</li>
    <ul>
      <li>步骤2-1</li>
      <li>步骤2-2</li>
    </ul>
  </li>
</ol>
```

<ol>
  <li>步骤1</li>
  <li>步骤2</li>
    <ul>
      <li>步骤2-1</li>
      <li>步骤2-2</li>
    </ul>
  </li>
</ol>




## 文本格式化标签

| 标签       | 描述                                  |
| :--------- | :------------------------------------ |
| `<b>`      | 粗体文本。                            |
| `<big>`    | 定义大号字。                          |
| `<em>`     | 定义着重文字。                        |
| `<i>`      | 定义斜体字。                          |
| `<small>`  | 定义小号字。                          |
| `<strong>` | 定义加重语气。                        |
| `<sub>`    | 定义下标字。                          |
| `<sup>`    | 定义上标字。                          |
| `<ins>`    | 定义插入字。                          |
| `<del>`    | 定义删除字。                          |
| `<s>`      | *不赞成使用。*使用 `<del> `代替。     |
| `<strike>` | *不赞成使用。*使用 `<del>` 代替。     |
| `<u>`      | *不赞成使用。*使用样式（style）代替。 |





### `<em>` 斜体强调

`<em>` 定义着重文字，强调，显示为**斜体**效果。

```html
<p>I am glad you weren't late.</p>
<p>I am <em>glad</em> you weren't <em>late</em>.</p>
```

<p>I am glad you weren't late.</p>
<p>I am <em>glad</em> you weren't <em>late</em>.</p>

第一句话语气真诚。第二句话具有讽刺性而且有隐含的攻击性，表达对一个人迟到的恼怒。

> 如果仅仅是为了斜体风格，应该使用 `<span>` 元素和 CSS，或者 `<i>` 元素，而不是 `<em>` 元素。



### `<strong>` 粗体强调

`<strong>` 强调重要的词，显示为**粗体**。

可以将 `<strong>` 和 `<em>` 嵌套在其他的标签中：

```html
<p>This liquid is <strong>highly toxic</strong> —
if you drink it, <strong>you may <em>die</em></strong>.</p>
```

This liquid is **highly toxic** — if you drink it, **you may *die***.

> 仅仅为了获得粗体风格，应该使用 `<span>` 元素和一些 CSS，或者是 `<b>` 元素。



### `<i>` 、`<b>` 和 `<u>` 

`<i>` 、`<b>` 和 `<u>` 的情况有点复杂。它们出现在人们要在文本中使用粗体、斜体、下划线但 CSS 仍然不被完全支持的时期。

像这样的元素，仅仅影响表象而且没有语义，被称为**表象元素（presentational elements）**并且不应该再被使用。因为语义对可访问性、SEO（搜索引擎优化）等非常重要。

- `<i>` 被用来传达传统上用斜体表达的意义：外国文字（学名、舶来词等），分类名称，技术术语，一种思想……
- `<b>` 被用来传达传统上用粗体表达的意义：关键字，产品名称，引导句……
- `<u>` 被用来传达传统上用下划线表达的意义：专有名词，拼写错误……

> 警告：**很容易把下划线和超链接联系起来**。因此，在 Web上，最好只在链接上使用下划线。当语义适合时使用 `<u>` 元素，但是有时候在Web上用 CSS 改变下划线默认的的样式更加合适。

```html
<!-- 学名 -->
<p>
  红喉北蜂鸟（学名：<i>Archilocus colubris</i>）
  是北美东部最常见的蜂鸟品种。
</p>

<!-- 舶来词 -->
<p>
  菜单上有好多舶来词汇，比如 <i lang="uk-latn">vatrushka</i>（东欧乳酪面包）,
  <i lang="id">nasi goreng</i>（印尼炒饭）以及<i lang="fr">soupe à l'oignon</i>（法式洋葱汤）。
</p>

<!-- 已知的错误书写 -->
<p>
  总有一天我会改掉写<u>措字</u>的毛病。
</p>

<!-- 系列说明文字中需要突出的文字 -->
<ol>
  <li>
    <b>切</b>下两片面包，
  </li>
  <li>
    在两片面包中间<b>夹入</b>一片西红柿和一片生菜叶。
  </li>
</ol>
```

红喉北蜂鸟（学名：*Archilocus colubris*） 是北美东部最常见的蜂鸟品种。

菜单上有好多舶来词汇，比如 *vatrushka*（东欧乳酪面包）, *nasi goreng*（印尼炒饭）以及*soupe à l'oignon*（法式洋葱汤）。

总有一天我会改掉写<u>措字</u>的毛病。

1. **切**下两片面包，
2. 在两片面包中间**夹入**一片西红柿和一片生菜叶。





