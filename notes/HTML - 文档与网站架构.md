

# 六、文档与网站架构

## 文档的基本组成部分

倾向于使用类似的标准组件：

- 页眉

- 导航栏：指向网站各个主要区段的超链接。通常用菜单按钮、链接或标签页表示。

- 主内容：中心的大部分区域是当前网页大多数的独有内容。

- 侧边栏：一些外围信息、链接、引用、广告等。通常与主内容相关，还可能存在其他的重复元素，如辅助导航系统。

- 页脚：和标题一样，页脚是放置公共信息（比如：版权声明或联系方式）的，一般使用较小字体，且通常为次要内容。 还可以通过提供快速访问链接来进行 SEO。




## 用于构建内容的 HTML



结构标签可以实现语义化的标签，专门用于标识页面的不同结构。为了实现语义化标记，HTML 提供了明确这些区段的专用标签：

- `<header>` ：页眉。简介形式的内容。如果是 `<body>` 的子元素，那么就是网站的全局页眉。如果是 `<article>` 或 `<section>` 的子元素，那么它是这些部分特有的页眉（此 `<header>` 非彼 标题）。
- `<nav>` ：导航栏。不应包含二级链接等内容。
- `<main>` ：主内容。存放每个页面独有的内容。每个页面上只能用一次 `<main>` ，且直接位于`<body>` 中。最好不要把它嵌套进其它元素。主内容中还可以有各种子内容区段，可用 `<article>` 、`<section>` 和 `<div>` 等元素表示。
- `<article>` 包围的内容即一篇文章，与页面其它部分无关（比如一篇博文）。
- `<section>` 与 `<article>`  类似，但 `<section>` 更适用于组织页面使其按功能（比如迷你地图、一组文章标题和摘要）分块。一般的最佳用法是：以 [标题](https://developer.mozilla.org/en-US/Learn/HTML/Howto/Set_up_a_proper_title_hierarchy) 作为开头；也可以把一篇 `<article>` 分成若干部分并分别置于不同的 `<section>` 中，也可以把一个区段 `<section>` 分成若干部分并分别置于不同的 `<article>` 中，取决于上下文。
- `<aside>` ：侧边栏，经常嵌套在 `<main>` 中。包含一些间接信息（术语条目、作者简介、相关链接，等等）。
- `<footer>` ：页脚。

例子：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>二次元俱乐部</title>
    <link href="" rel="stylesheet">
    <link href="" rel="stylesheet">
    <link href="style.css" rel="stylesheet">
  </head>

  <body>
    <header> <!-- 本站所有网页的统一主标题 -->
      <h1>聆听电子天籁之音</h1>
    </header>
    
    <nav> <!-- 本站统一的导航栏 -->
      <ul>
        <li><a href="#">主页</a></li>
        <!-- 共n个导航栏项目，省略…… -->
      </ul>

      <form> <!-- 搜索栏是站点内导航的一个非线性的方式。 -->
        <input type="search" name="q" placeholder="要搜索的内容">
        <input type="submit" value="搜索">
      </form>
    </nav>
    
    <main> <!-- 网页主体内容 -->
      <article>
        <!-- 此处包含一个 article（一篇文章），内容略…… -->
      </article>
      
      <aside> <!-- 侧边栏在主内容右侧 -->
        <h2>相关链接</h2>
        <ul>
          <li><a href="#">这是一个超链接</a></li>
          <!-- 侧边栏有n个超链接，略略略…… -->
        </ul>
      </aside>
    </main>
    
    <footer> <!-- 本站所有网页的统一页脚 -->
      <p>© 2050 某某保留所有权利</p>
    </footer>
  </body>
</html>
```



## HTML 布局元素细节

### 无语义元素

对于一些要组织的项目或要包装的内容，现有的语义元素可能均不能很好对应。有时候你可能只想将一组元素作为一个单独的实体来修饰来响应单一的用 [CSS](https://developer.mozilla.org/zh-CN/docs/Glossary/CSS) 或 [JavaScript](https://developer.mozilla.org/zh-CN/docs/Glossary/JavaScript)。为了应对这种情况，HTML提供了 `<div>` 和 `<span>` 元素。应配合使用 `class` 属性提供一些标签，使这些元素能易于查询。

无语义元素的应用：最好只用于找不到更好的语义元素时，或者不想增加特定的意义时。尽可能少用。

`<span>` 是一个内联的无语义元素。

```html
<p>国王喝得酩酊大醉，在凌晨 1 点时才回到自己的房间，踉跄地走过门口。<span class="editor-note">[编辑批注：此刻舞台灯光应变暗]</span>.</p>
```

 `<div>` 是一个块级无语义元素。下例中，一个电子商务网站页面上有一个一直显示的购物车组件。

```html
<div class="shopping-cart">
  <h2>购物车</h2>
  <ul>
    <li>
      <p><a href=""><strong>银耳环</strong></a>：$99.95.</p>
      <img src="../products/3333-0985/" alt="Silver earrings">
    </li>
    <li>
      ...
    </li>
  </ul>
  <p>售价：$237.89</p>
</div>
```

这里不应使用 `<aside>` ，因为它和主内容并没有必要的联系（你想在任何地方都能看到它）。甚至不能用 `<section>` ，因为它也不是页面上主内容的一部分。所以在这种情况下就应使用 `<div>`，为满足无障碍使用特征，还应为购物车的标题设置一个可读标签。

> **警告：** `<div>` 非常便利但容易被滥用。由于它们没有语义值，会使 HTML 代码变得混乱。要小心使用，只有在没有更好的语义方案时才选择它，而且要尽可能少用， 否则文档的升级和维护工作会非常困难。





### HTML 换行

在不产生一个新段落的情况下进行**换行**，使用 `<br />`  标签。

```html
<p>This is<br />a para<br />graph with line breaks</p>
```

```
This is
a para
graph with line breaks
```

>  `<br />` 元素是空元素，没有结束标签。



### HTML 水平线

`<hr />` 标签在 HTML 页面中创建水平线，可用于分隔内容。

```
<p>This is a paragraph</p>
<hr />
<p>This is a paragraph</p>
<hr />
<p>This is a paragraph</p>
```

**提示：**使用水平线 (`<hr />` 标签) 来分隔文章中的小节是一个办法（但并不是唯一的办法）。



## 框架  `<iframe>` 



内联框架元素 `<iframe>` 表示嵌套的浏览器上下文，能够将另一个 HTML 页面嵌入到当前页面中。

每个嵌入的浏览上下文都有自己的会话历史记录(session history)和 DOM树。包含嵌入内容的浏览上下文称为*父级浏览上下文*。顶级浏览上下文（没有父级）通常是由 `Window` 对象表示的浏览器窗口。

```html
<iframe src="URL"></iframe>
```

属性：

| 属性        | 描述                                    |
| ----------- | --------------------------------------- |
| height      | 高度                                    |
| frameborder | 是否显示边框，设置属性值为 "0" 移除边框 |
| src         | URL指向不同的网页。                     |
| width       | 宽度                                    |


