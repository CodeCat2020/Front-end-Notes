







## 什么是 XHTML?

XHTML 指的是可扩展超文本标记语言，以 XML 格式编写的 HTML。

- XHTML 与 HTML 4.01 几乎是相同的
- XHTML 是更严格更纯净的 HTML 版本
- XHTML 是 2001 年 1 月 发布的 W3C 推荐标准
- XHTML 得到所有主流浏览器的支持



## 为什么使用 XHTML?

因特网上的很多页面包含了"糟糕"的 HTML。小型设备往往缺乏解释"糟糕"的标记语言的资源和能力。

下面的代码即使没有遵守 HTML 规则，运行起来也非常正常：

```html
<html>
	<head>
		<meta charset="utf-8">
		<title>这是一个不规范的 HTML</title>
	<body>
		<h1>不规范的 HTML
		<p>这是一个段落
	</body>
```

XML 是一种必须正确标记且格式良好的标记语言。通过结合 XML 和 HTML 的长处，开发出了 XHTML。





## XHTML 与 HTML 的区别



HTML 是一种基于 Web 网页的设计语言， XHTML 是一种基于 XML 、语法严格、标准的设计语言。
两者主要的不同是 XHTML 元素必须正确地嵌套，元素必须关闭，标签必须小写，必须有根元素； HTML 没有这些限制。



### 文档结构

在 XHTML 文档中：

- XHTML DOCTYPE 是*强制性的*
- `<html>` 中的 XML namespace 属性是*强制性的*
- `<html>` 、 `<head>` 、`<title>` 和 `<body>` 元素也必须存在，并且必须使用 `<html>` 中的 xmlns 属性为文档规定 xml 命名空间。

下面的例子展示了带有最少的必需标签的 XHTML 文档：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
      <meta charset="utf-8">
      <title>文档标题</title>
    </head>
 
    <body>
    文档内容
    </body> 
</html>
```



### 元素语法

- XHTML 元素必须***正确嵌套***。

  ```html
  <b><i>粗体和斜体文本</b></i>	<!--在 HTML 中，元素可以不互相嵌套。-->
  <b><i>粗体和斜体文本</i></b>	<!--在 XHTML 中，所有元素必须合理嵌套。-->
  ```

- XHTML 元素必须***始终关闭***

  错误示例：

  ```html
  <p>这是一个段落
  <br>
  ```

  正确示例：

  ```html
  <p>这是一个段落</p>
  <!--空元素必须包含关闭标签-->
  <br />
  ```

- XHTML 元素***必须小写***

- XHTML 文档**必须有*一个根元素***



### 属性语法

- XHTML 属性必须**使用*小写***

  ```html
  <table WIDTH="100%">	<!--错误示例-->
  <table width="100%">	<!--正确示例-->
  ```

- XHTML 属性值必须**用*引号包围***

- XHTML 属性***禁止*最小化**

  错误示例：

  ```html
  <input checked>
  <input readonly>
  <input disabled>
  <option selected>
  ```

  正确示例：

  ```html
  <!--不允许属性简写-->
  <input checked="checked">
  <input readonly="readonly">
  <input disabled="disabled">
  <option selected="selected">
  ```



## 如何将 HTML 转换为 XHTML

1. 添加一个 XHTML <!DOCTYPE> 到你的网页中
2. 添加 xmlns 属性添加到每个页面的 html 元素中。
3. 改变所有的元素为小写
4. 关闭所有的空元素
5. 修改所有的属性名称为小写
6. 所有属性值添加引号





