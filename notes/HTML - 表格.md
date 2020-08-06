

# 表格  `<table>` 

表格由 `<table>` 标签来定义。

- 每个表格均有若干行（由 `<tr>` 标签定义）
- 每行被分割为若干单元格（由 `<td>` 标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

```html
<table border="1">
<tr>
<td>row 1, cell 1</td>
<td>row 1, cell 2</td>
</tr>
<tr>
<td>row 2, cell 1</td>
<td>row 2, cell 2</td>
</tr>
</table>
```

在浏览器显示如下：

| row 1, cell 1 | row 1, cell 2 |
| ------------- | ------------- |
| row 2, cell 1 | row 2, cell 2 |





| 标签         | 描述                 |
| :----------- | :------------------- |
| `<table>`    | 定义表格             |
| `<th>`       | 定义表格的表头       |
| `<tr>`       | 定义表格的行         |
| `<td>`       | 定义表格单元         |
| `<caption>`  | 定义表格标题         |
| `<colgroup>` | 定义表格列的组       |
| `<col>`      | 定义用于表格列的属性 |
| `<thead>`    | 定义表格的页眉       |
| `<tbody>`    | 定义表格的主体       |
| `<tfoot>`    | 定义表格的页脚       |

table元素的子元素：没有col。col是作为colgroup(定义表格中的列)的子元素存在的！







##   `<table>` 属性

| 属性                                                         | 值                                                | 描述                                                         |
| :----------------------------------------------------------- | :------------------------------------------------ | :----------------------------------------------------------- |
| [align](https://www.runoob.com/tags/att-table-align.html)    | left center right                                 | HTML5 不支持。HTML 4.01 已废弃。 规定表格相对周围元素的对齐方式。 |
| [bgcolor](https://www.runoob.com/tags/att-table-bgcolor.html) | *rgb(x,x,x) #xxxxxx colorname*                    | HTML5 不支持。HTML 4.01 已废弃。 规定表格的背景颜色。        |
| [**border**](https://www.runoob.com/tags/att-table-border.html) | 1 ""                                              | 规定表格单元是否拥有边框。                                   |
| [cellpadding](https://www.runoob.com/tags/att-table-cellpadding.html) | *pixels*                                          | HTML5 不支持。规定单元边沿与其内容之间的空白。               |
| [cellspacing](https://www.runoob.com/tags/att-table-cellspacing.html) | *pixels*                                          | HTML5 不支持。规定单元格之间的空白。                         |
| [frame](https://www.runoob.com/tags/att-table-frame.html)    | void above below hsides lhs rhs vsides box border | HTML5 不支持。规定外侧边框的哪个部分是可见的。               |
| [rules](https://www.runoob.com/tags/att-table-rules.html)    | none groups rows cols all                         | HTML5 不支持。规定内侧边框的哪个部分是可见的。               |
| [summary](https://www.runoob.com/tags/att-table-summary.html) | *text*                                            | HTML5 不支持。规定表格的摘要。                               |
| [width](https://www.runoob.com/tags/att-table-width.html)    | *pixels %*                                        | HTML5 不支持。规定表格的宽度。                               |



### cellpadding 属性

在使用 table 表现数据时，有时候表现出来的会比自己实际设置的宽度要宽，为此需要设置下面哪些属性值？

答：设置 cellpadding=”0″ 和 cellspacing=”0″。但是，从实用角度出发，最好使用 CSS 来添加内边距。





### border 属性

使用 border 属性定义表格**边框线的粗细**，单位是 **px**。

```html
<table border="5">
	<tr>
		<td>Row 1, cell 1</td>
		<td>Row 1, cell 2</td>
	</tr>
</table>
```

<table border="5">
	<tr>
		<td>Row 1, cell 1</td>
		<td>Row 1, cell 2</td>
	</tr>
</table>









##  `<th>` 表头

表格的表头使用 `<th>` 标签进行定义。

水平标题：

```html
<table border="1">
	<tr>
        <!--大多数浏览器会把表头显示为粗体居中的文本-->
		<th>Heading</th>
		<th>Another Heading</th>
	</tr>
	<tr>
		<td>row 1, cell 1</td>
		<td>row 1, cell 2</td>
	</tr>
	<tr>
		<td>row 2, cell 1</td>
		<td>row 2, cell 2</td>
	</tr>
</table>
```

在浏览器显示如下：

| Heading       | Another Heading |
| ------------- | --------------- |
| row 1, cell 1 | row 1, cell 2   |
| row 2, cell 1 | row 2, cell 2   |

垂直标题：

```html
<table border="1">
  <tr>
    <th>First Name:</th>
    <td>Bill Gates</td>
  </tr>
  <tr>
    <th>Telephone:</th>
    <td>555 77 854</td>
  </tr>
</table>
```

浏览器显示：

<table border="1">
  <tr>
    <th>First Name:</th>
    <td>Bill Gates</td>
  </tr>
  <tr>
    <th>Telephone:</th>
    <td>555 77 854</td>
  </tr>
</table>







## 空单元格

如果某个单元格是空的（没有内容），浏览器可能无法显示出这个单元格的边框，比如边框没有被显示出来。

```html
<table border="1">
	<tr>
		<td>row 1, cell 1</td>
		<td>row 1, cell 2</td>
	</tr>
	<tr>
		<td></td>
		<td>row 2, cell 2</td>
	</tr>
</table>
```

浏览器可能会这样显示：

<div align="center"> <img src="pics/前端-HTML-table_td_empty.png"/></div><br>

为了避免这种情况，在空单元格中添加一个空格占位符。

```html
<table border="1">
	<tr>
		<td>row 1, cell 1</td>
		<td>row 1, cell 2</td>
	</tr>
	<tr>
		<td>&nbsp;</td>
		<td>row 2, cell 2</td>
	</tr>
</table>
```

在浏览器中显示如下：

| row 1, cell 1 | row 1, cell 2 |
| ------------- | ------------- |
|               | row 2, cell 2 |







## 跨行和跨列

`colspan` 跨列。比如，`colspan="2"` 使一个单元格的宽度是两个单元格。

```html
<table border="1">
<caption>单元格跨两列</caption>
<tr>
  <th>Name</th>
  <th colspan="2">Telephone</th>
</tr>
<tr>
  <td>Bill Gates</td>
  <td>555 77 854</td>
  <td>555 77 855</td>
</tr>
</table>
```

<table border="1">
<caption>单元格跨两列</caption>
<tr>
  <th>Name</th>
  <th colspan="2">Telephone</th>
</tr>
<tr>
  <td>Bill Gates</td>
  <td>555 77 854</td>
  <td>555 77 855</td>
</tr>
</table>


`rowspan` 跨列。

```html
<table border="1">
<caption>单元格跨两行</caption>
<tr>
  <th>First Name:</th>
  <td>Bill Gates</td>
</tr>
<tr>
  <th rowspan="2">Telephone:</th>
  <td>555 77 854</td>
</tr>
<tr>
  <td>555 77 855</td>
</tr>
</table>
```

<table border="1">
<caption>单元格跨两行</caption>
<tr>
  <th>First Name:</th>
  <td>Bill Gates</td>
</tr>
<tr>
  <th rowspan="2">Telephone:</th>
  <td>555 77 854</td>
</tr>
<tr>
  <td>555 77 855</td>
</tr>
</table>


**如何确定表格的行数和列数？**

 `<tr>` 的数量表示行数。一行中 `<td>` 最多的数量表示列数。




##  `<col>` 和 `<colgroup>` 

如果想统一整列数据的样式，通常需要在列中的每个 `<td>` 或 `<th>` 上定义样式，或者使用一个复杂的选择器，比如 [`:nth-child()`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-child())。

```html
<table>
  <tr>
    <th>Data 1</th>
    <th style="background-color: yellow">Data 2</th>
  </tr>
  <tr>
    <td>row 1, cell 1</td>
    <td style="background-color: yellow">row 1, cell 2</td>
  </tr>
</table>
```

<table>
  <tr>
    <th>Data 1</th>
    <th style="background-color: yellow">Data 2</th>
  </tr>
  <tr>
    <td>row 1, cell 1</td>
    <td style="background-color: yellow">row 1, cell 2</td>
  </tr>
</table>

 `<col>` 和 `<colgroup>` 元素可以定义整列数据的样式信息。

 `<col>` 元素被规定包含在 `<colgroup>` 容器中，而 `<colgroup>`  在  `<table>`  标签的下方。

下面代码的显示效果与上例相同。使用两个 `<col>` 来定义“列的样式”，每个 `<col>` 制定对应列的样式。即使没有任何样式，仍需要添加一个空的 `<col>` 元素。

```html
<table>
  <colgroup>
    <col>
    <col style="background-color: yellow">
  </colgroup>
  <tr>
    <th>Data 1</th>
    <th>Data 2</th>
  </tr>
  <tr>
    <td>row 1, cell 1</td>
    <td style="background-color: yellow">row 1, cell 2</td>
  </tr>
</table>
```

也可以只使用一个 `<col>` 元素，不过需要包含 span 属性，`span` 需要一个无单位的数字值，用来指定样式应用的所在列。

```html
<colgroup>
  <col style="background-color: yellow" span="2">
</colgroup>
```





# 高级特性和可访问性

## `<caption>` 标题

 `<caption>` 元素定义表格标题，应该把 `<caption>` 元素放入  `<table>` 元素的下面。

```html
<table>
  	<caption>表格标题</caption>
	<tr>
		<td>row 1, cell 1</td>
		<td>row 1, cell 2</td>
	</tr>
	<tr>
		<td>row 2, cell 1</td>
		<td>row 2, cell 2</td>
	</tr>
</table>
```

<table>
  	<caption>表格标题</caption>
	<tr>
		<td>row 1, cell 1</td>
		<td>row 1, cell 2</td>
	</tr>
	<tr>
		<td>row 2, cell 1</td>
		<td>row 2, cell 2</td>
	</tr>
</table>



## 表格结构

 `<thead>`, `<tfoot>` 和 `<tbody>` 结构

如果表格结构有点复杂，使用 `<thead>`，`<tfoot>` 和 `<tbody>` , 把表格中的部分标记为表头、页脚、正文部分。

> 所有表都有 `<tbody>` ，如果没有指明，则 `<tbody>` 是隐式的。 `<tbody>` 可以让编码者更好地控制表格结构和样式。



## 嵌套表格

可行，但不建议，因为这种做法会使标记看上去很难理解，对使用屏幕阅读的用户来说，可访问性也降低了。

```html
<table id="table1">
  <tr>
    <th>title1</th>
    <th>title2</th>
  </tr>
  <tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
  </tr>
  <tr>
    <td>cell4</td>
    <td>cell5</td>
  </tr>
</table>
```

<table id="table1">
  <tr>
    <th>title1</th>
    <th>title2</th>
  </tr>
  <tr>
    <td id="nested">
      <table id="table2">
        <tr>
          <td>cell1</td>
          <td>cell2</td>
        </tr>
      </table>
    </td>
    <td>cell2</td>
  </tr>
  <tr>
    <td>cell4</td>
    <td>cell5</td>
  </tr>
</table>





## 对于视力受损的用户的表格

### 使用列和行的标题



屏幕阅读设备会识别所有的标题，然后在它们和它们所关联的单元格之间产生编程关联。列和行标题的组合将标识和解释每个单元格中的数据，以便屏幕阅读器用户可以类似于视力正常的用户的操作来理解表格。

### scope 属性

本篇文章的一个新话题是 `scope` 属性，可以添加在 `<th>` 元素中，用来帮助屏幕阅读设备更好地理解那些标题单元格，这个标题单元格到底是列标题呢，还是行标题。比如： 回顾我们之前的支出记录示例，你可以明确地将列标题这样定义：

```html
<thead>
  <tr>
    <th scope="col">Purchase</th>
    <th scope="col">Location</th>
    <th scope="col">Date</th>
    <th scope="col">Evaluation</th>
    <th scope="col">Cost (€)</th>
  </tr>
</thead>
```

以及每一行都可以这样定义一个行标题 (如果我们已经使用了 th 和 td 元素):

```html
<tr>
  <th scope="row">Haircut</th>
  <td>Hairdresser</td>
  <td>12/09</td>
  <td>Great idea</td>
  <td>30</td>
</tr>
```

屏幕阅读设备会识别这种结构化的标记，并一次读出整列或整行，比如：

`scope` 还有两个可选的值 ： `colgroup` 和 `rowgroup`。这些用于位于多个列或行的顶部的标题。 如果你回顾这部分文章开始部分的 "Items Sold August 2016" 表格。你会看到 "Clothes" 单元格在"Trousers", "Skirts", 和 "Dresses" 单元格的上面。这几个单元格都应该被标记为 ( `<th>` )，但是 "Clothes" 是一个位于顶部且定义了其他三个子标题的标题。 因此 "Clothes" 应该有一个 `scope="colgroup"`属性，而另外三个子标题应该有 `scope="col"`属性。

### id 和标题属性



如果要替代 `scope` 属性，可以使用 `id` 和 `headers` 属性来创造标题与单元格之间的联系。使用方法如下:

1. 为每个 `<th>`  元素添加一个唯一的 `id` 。
2. 为每个  `<td>` 元素添加一个 `headers` 属性。每个单元格的`headers` 属性需要包含它从属于的所有标题的id，之间用空格分隔开。

这会给你的HTML表格中每个单元格的位置一个明确的定义。像一个电子表格一样，通过 headers 属性来定义属于哪些行或列。为了让它工作良好，表格同时需要列和行标题。

回到我们的花费成本示例，前两个片段可以重写为：

```html
<thead>
  <tr>
    <th id="purchase">Purchase</th>
    <th id="location">Location</th>
    <th id="date">Date</th>
    <th id="evaluation">Evaluation</th>
    <th id="cost">Cost (€)</th>
  </tr>
</thead>
<tbody>
<tr>
  <th id="haircut">Haircut</th>
  <td headers="location haircut">Hairdresser</td>
  <td headers="date haircut">12/09</td>
  <td headers="evaluation haircut">Great idea</td>
  <td headers="cost haircut">30</td>
</tr>

  ...

</tbody>
```

> **注意**: 这个放进为标题单元格和数据单元格之间创造了非常精确的联系。但是这个方法使用了大量的标记，所以容错率比较低。使用 `scope` 的方法对于大多数表格来说，也够用了。