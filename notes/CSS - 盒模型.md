





# 二、CSS 语言基础



## 盒模型



**什么是 CSS 盒模型？**

所有的 HTML 元素都可以看作盒子。盒模型在设计和布局时使用，模型定义了盒的每个部分。

完整的 CSS 盒模型应用于块级盒子，内联盒子只使用盒模型中定义的部分内容。



**盒模型的各个部分**

- **外边距（margin）** - 盒子和其他元素之间的空白区域。可以设置盒子与相邻元素的间距。
- **边框（border）** - 围绕在内边距和内容外的边框。可以设置边框的宽窄、样式和颜色。
- **内边距（padding，填充）** - 包围在内容区域外部的空白区域。可以设置盒子内容区与边框的间距。
- **内容（content）** - 用来显示内容。大小可以通过设置 `width` 和 `height`。

<div align="center"> <img src="pics/前端-CSS-盒模型-box-model.gif"/> </div><br>



### 两种模型

为了增加一些额外的复杂性，有两种盒模型：标准盒模型和替代（IE）的盒模型。





**标准盒模型** 

在标准模型中，指定一个 CSS 元素的 `width` 和 `height`，实际设置的是内容区域的宽度和高度。padding 和 border 再加上设置的 `width` 和 `height` 一起决定整个盒子的大小。

> margin 不计入实际大小，盒子的范围到边框为止。margin 会影响盒子在页面所占空间，但是影响的是盒子外部空间。

```css
.box {
  width: 350px;
  height: 150px;
  margin: 25px;
  padding: 25px;
  border: 5px solid black;
}
```

盒子宽度 = 410px (350 + 25 + 25 + 5 + 5)，盒子高度 = 210px (150 + 25 + 25 + 5 + 5)。

<div align="center"> <img src="pics/前端-CSS-盒模型-standard-box-model.png"/> </div><br>



**替代（IE）盒模型**

使用这个模型，所有宽度都是可见宽度，所以内容宽度是该宽度减去边框和填充部分。

使用上面相同的样式得到 (width = 350px, height = 150px)。

<div align="center"> <img src="pics/前端-CSS-盒模型-alternate-box-model.png"/> </div><br>



### 简写样式

CSS 为 boder、padding 和 margin 分别规定了简写属性，通过一条声明就可以完成设定。在每个简写声明中，属性值的顺序都是**上、右、下、左**。

```css
{margin-top:5px; margin-right:10px; margin-bottom:12px; margin-left:8px;}
```

使用简写属性，则可以简写为这样：

```css
{margin:5px 10px 12px 8px;}
```

注意，两个值之间有**空格**，但不能是其他分隔符。

```css
{margin:5px, 10px, 12px, 8px;}	/*错误写法，两个值之间只能用空格分隔*/
```

甚至，不用把值全都写出来——如果哪个值没有写，那就使用对边的值。

```css
/*由于没有写最后一个值（左边的值），所以左边就会使用右边的值，即10px。*/
{margin:12px 10px 6px;}
```

在下面的例子中，只写了两个值，上和右，因此缺少的下和左就会被设定为 12px 和 10px。

```css
{margin:12px 10px;}
```

如果只写一个值，那么4 个边都取这个值。

```css
{margin:12px;}
```





### margin 外边距

外边距是盒子周围一圈看不到的空间。外边距属性值可以为正也可以为负。设置负值会导致和其他内容重叠。无论使用标准模型还是替代模型，外边距总是在计算可见部分后额外添加。

| 属性                                                         | 描述                                       |
| :----------------------------------------------------------- | :----------------------------------------- |
| [margin](https://www.runoob.com/cssref/pr-margin.html)       | 简写属性。在一个声明中设置所有外边距属性。 |
| [margin-bottom](https://www.runoob.com/cssref/pr-margin-bottom.html) | 设置元素的下外边距。                       |
| [margin-left](https://www.runoob.com/cssref/pr-margin-left.html) | 设置元素的左外边距。                       |
| [margin-right](https://www.runoob.com/cssref/pr-margin-right.html) | 设置元素的右外边距。                       |
| [margin-top](https://www.runoob.com/cssref/pr-margin-top.html) | 设置元素的上外边距。                       |







**外边距折叠**

垂直方向上的外边距会叠加：相邻的两个盒子的上下外边距会相互重叠，直至一个外边距碰到另一个元素的边框。**较宽的外边距决定两个元素最终离多远**。这个过程就叫外边距叠加。

外边距叠加原因：如果有一连串段落都被应用了相同的样式，位于中间的段落不需要两个外边距加起来那么宽的间距。因此，相邻的外边距叠加起来是最合理的，哪个外边距宽，就以哪个外边距作为段间距。

> 叠加的只是垂直外边距，<u>水平外边距不叠加</u>。对于水平相邻的元素，它们的水平间距是相邻外边距之和。

折叠结果遵循下列计算规则：

- 当两个相邻的外边距都是正数时，折叠结果是它们两者中较大的值。
- 当两个相邻的外边距都是负数时，折叠结果是两者中绝对值较大的值。
- 当两个外边距一正一负时，折叠结果是两者相加的和。



### border 边框

border 是简写属性，有 3 个相关属性，编写顺序是：

- 宽度（border-width）。可以使用 thin、medium 和 thick 等文本值，也可以使用除百分比和负值之外的任何绝对值。
- 样式（border-style）。有 **none**、hidden、dotted、dashed、solid、double、groove、ridge、inset 和 outset 等文本值。
- 颜色（border-color）。可以使用任意颜色值，包括 RGB、HSL、十六进制颜色值和颜色关键字。


分别设置每边的宽度、颜色和样式，可以使用：

- [`border-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top)
- [`border-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right)
- [`border-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom)
- [`border-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left)

例子：

```css
p{ border:5px solid red;}	/*正确写法，简写属性要按照顺序编写*/
```

border 属性少于三个时，按照值的类型确定样式。比如，border:none —— 边框样式无；border:0 —— 边框宽度为 0。



### padding 内边距

CSS 盒模型中 padding 是透明的，这部分可以显示背景。

| 属性                                                         | 说明                                       |
| :----------------------------------------------------------- | :----------------------------------------- |
| [padding](https://www.runoob.com/cssref/pr-padding.html)     | 使用简写属性设置在一个声明中的所有填充属性 |
| [padding-bottom](https://www.runoob.com/cssref/pr-padding-bottom.html) | 设置元素的底部填充                         |
| [padding-left](https://www.runoob.com/cssref/pr-padding-left.html) | 设置元素的左部填充                         |
| [padding-right](https://www.runoob.com/cssref/pr-padding-right.html) | 设置元素的右部填充                         |
| [padding-top](https://www.runoob.com/cssref/pr-padding-top.html) | 设置元素的顶部填充                         |





### 总结

网页设计中常听的属性名：内容(content)、填充(padding)、边框(border)、边界(margin)， CSS盒子模式都具备这些属性。

- 标准的 CSS 盒模型
  - 盒子宽度 = 内容的宽度 width + 边框的宽度 border + 内边框的宽度 padding
  - width = content 的宽度
- IE 盒模型：
  - 盒子宽度 = width
  - width = content + padding-Left + padding-right + border-left + border-right





## 显示 display

在 CSS1 中，display 属性规定元素应该生成的框的类型。默认值为 inline，不能被继承。JS 语法为：*object*.style.display="inline"。

支持的浏览器：Chrome 4.0、IE 8.0、FireFox 3.0、Safari 3.1、Opera 7.0。

display 的属性值：

| 值                 | 描述                                                         |
| :----------------- | :----------------------------------------------------------- |
| **none**           | 不显示，**不为被隐藏的对象保留物理空间**                     |
| **block**          | 显示为块级元素，元素前后带有换行符。                         |
| **inline**         | 默认。**显示为内联元素**，元素前后没有换行符。               |
| **inline-block**   | 行内块元素。（CSS2.1 ）                                      |
| list-item          | 指定对象为列表项目。                                         |
| run-in             | 根据上下文作为块级元素或内联元素显示。（CSS3）               |
| compact            | 缺乏广泛支持，CSS2.1 删除。                                  |
| marker             | 缺乏广泛支持，CSS2.1 删除。                                  |
| **table**          | 作为块级表格来显示（类似 `<table>`），表格前后带有换行符。（CSS2） |
| inline-table       | 作为内联表格来显示（类似 `<table>`），表格前后没有换行符。（CSS2） |
| table-row-group    | 作为一个或多个行的分组来显示（类似 `<tbody>`）。（CSS2）     |
| table-header-group | 作为一个或多个行的分组来显示（类似 `<thead>`）。（CSS2）     |
| table-footer-group | 作为一个或多个行的分组来显示（类似 `<tfoot>`）。（CSS2）     |
| table-row          | 作为一个表格行显示（类似 `<tr>`）。（CSS2）                  |
| table-column-group | 作为一个或多个列的分组来显示（类似 `<colgroup>`）。（CSS2）  |
| table-column       | 作为一个单元格列显示（类似 `<col>`）。（CSS2）               |
| table-cell         | 作为一个表格单元格显示（类似 `<td>` 和 `<th>`）。（CSS2）    |
| table-caption      | 作为一个表格标题显示（类似 `<caption>`）。（CSS2）           |
| inherit            | 从父元素继承 display 属性的值。                              |

box： 将对象作为弹性伸缩盒显示。（伸缩盒最老版本）（CSS3） 
inline-box： 将对象作为内联块级弹性伸缩盒显示。（伸缩盒最老版本）（CSS3） 
flexbox： 将对象作为弹性伸缩盒显示。（伸缩盒过渡版本）（CSS3） 
inline-flexbox： 将对象作为内联块级弹性伸缩盒显示。（伸缩盒过渡版本）（CSS3） 
flex： 将对象作为弹性伸缩盒显示。（伸缩盒最新版本）（CSS3） 
inline-flex： 将对象作为内联块级弹性伸缩盒显示。（伸缩盒最新版本）（CSS3）





**`display:block`**

- 独占一行。默认情况下，宽度自动填满其父元素宽度。
- **可以设置 width，height 属性**。块级元素即使设置了宽度，仍然是独占一行。
- 可以设置 margin 和 padding 属性。

**`display:inline`**

- 不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。
- 设置 width，height 属性无效。
- 水平方向的 padding-left，padding-right，margin-left，margin-right 都产生边距效果；但竖直方向的 padding-top，padding-bottom，margin-top，margin-bottom 不会产生边距效果。

**`display:inline-block`**

- 将对象呈现为 inline 对象，但是对象的内容作为 block 对象呈现。
- 既具有 block 的宽度、高度特性又具有 inline 的同行特性。

**补充说明**

低版本 IE 本来是不支持 inline-block 的，所以在 IE 中对内联元素使用 display:inline-block，理论上 IE 是不识别的，但使用 display:inline-block 在 IE 下会触发 layout，从而使内联元素拥有了 display:inline-block 属性的表象。





## 可见性 visibility

在 CSS2 中， visibility 规定元素是否可见，默认值是 visible，可以被继承。JS 语法是：*object*.style.visibility="hidden"。

所有主流浏览器都支持 visibility 属性。IE（包括 IE8）没有版本支持属值"inherit"或"collapse"。

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| visible  | 默认值。元素是可见的。                                       |
| hidden   | 元素是不可见的。                                             |
| collapse | 当在表格元素中使用时，此值可删除一行或一列，但是它不会影响表格的布局。被行或列占据的空间会留给其他内容使用。如果此值被用在其他的元素上，会呈现为 "hidden"。 |
| inherit  | 规定应该从父元素继承 visibility 属性的值。                   |



## 背景 background

background 属性可以用来设定所有背景相关的值。声明中少写了哪个属性的值，就会使用相应属性的默认值。

在简写背景属性时遵循一些规则：

- `background-color` 只能在逗号之后指定。
- `background-size` 值只能包含在背景位置之后，用 '/' 字符分隔

当使用 `background` 简写属性时，属性值的顺序为：

| 属性                  | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| background-color      | 定义了元素的背景颜色                                         |
| background-image      | 描述了元素的背景图像（默认平铺重复显示）                     |
| background-repeat     | 控制图像的平铺行为。属性值如下：<br/>no-repeat：不平铺<br>repeat-x：水平重复<br/>repeat-y：垂直重复<br/>repeat：在两个方向重复 |
| background-attachment | 背景图像是否固定或者随着页面的其余部分滚动。<br/>scroll：背景在页面滚动时滚动<br/>fixed：<br/>local： |
| background-position   | 简写属性，改变图像在背景中的位置<br/>background-position-x 和 background-position-y |
| background-size       | 调整背景图像的大小，可以设置的值：<br/>长度或百分比值<br/>cover：完全覆盖盒子，仍然保持其高宽比<br/>contain：使图像的大小适合盒子内 |





### **背景颜色**





前景色会影响元素的内容和边框。当然，有一个前提条件，就是在使用 border 设定边框的样式和宽度，而没有设定边框颜色的情况下，边框会使用 color 属性设定的字体颜色。默认颜色是黑色。如果你想让边框的颜色有别于文本，就需要单独设定。

背景色扩展到元素的内容和内边距的下面。

```css
.box {
  background-color: #567895;
}

h2 {
  background-color: black;
  color: white;
}
span {
  background-color: rgba(255,255,255,.5);
}
```



### **背景图片**

```css
.a {
  background-image: url(balloons.jpg);
}

.b {
  background-image: url(star.png);
}
  
```

```html
<div class="wrapper">
  <div class="box a"></div>
  <div class="box b"></div>
</div>
```

**如果除了背景图像外，还指定了背景颜色，则图像将显示在颜色的顶部。**



### **图像平铺**

`background-repeat` 属性用于控制图像的平铺行为。可用的值是：

- `no-repeat` — 不重复。
- `repeat-x` —水平重复。
- `repeat-y` —垂直重复。
- `repeat` — 在两个方向重复。



**图像大小**

 [`background-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)属性，它可以设置长度或百分比值，来调整图像的大小以适应背景。

你也可以使用关键字:



### **背景图像定位**

background-position

- 关键字：top、right、center
- 长度值
- 百分比



该属性可有两个取值，第一个取值为背景图像与其容器在水平方向上的距离，第二个取值为背景图像与其容器在垂直方向上的距离。

参数：xpos ypos |x% y% |x y三种

- 若只有一个取值，则其第二个取值默认为：center|50%|容器高度的一半px。

- Xpos：规定水平方向的对齐方式，值有 left，right，center。

- Ypos：规定垂直方向的对齐方式，值有 top，bottom，center。

- x%：规定图片水平方向的距离。指的是父级容器的宽度减去图片的宽度后的差值的 x%。

  y%：对应 x%。

若属性取值用 left、center、right、top、bottom 表示，则该属性取值的顺序可以颠倒，否则其取值顺序不能颠倒。



**渐变背景**

```css
.a {
  background-image: linear-gradient(105deg, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);
}

.b {
  background-image: radial-gradient(circle, rgba(0,249,255,1) 39%, rgba(51,56,57,1) 96%);
  background-size: 100px 50px;
}
```

```html
<div class="wrapper">
  <div class="box a"></div>
  <div class="box b"></div>
</div>
```



**多个背景图像**

在单个属性值中指定多个 `background-image` 值，用逗号分隔每个值。

渐变可以与常规的背景图像很好地混合在一起。

其他 `background-*` 属性也可以用逗号分隔多个值。不同属性的每个值将与其他属性中相同位置的值匹配。

```css
background-image: url(image1.png), url(image2.png), url(image3.png), url(image1.png);
background-repeat: no-repeat, repeat-x, repeat;
background-position: 10px 20px,  top right;
```



**背景附加**

- `scroll`： 默认值，滚动页面时背景会滚动。滚动元素内容，背景不会移动。
- `fixed`：**固定**背景，滚动页面或元素内容时，背景不会滚动。始终保持在屏幕上的相同位置。
- `local`：CSS3 新增，可将元素的背景固定为实际的元素本身。因此，当滚动页面时，仅当元素这样做时元素的背景才会随之移动（带有 `position: fixed` 的元素不会）。滚动元素的内容时，背景将与其一起滚动。



**背景的可访问性**

把文字放在背景图片或颜色上面时，应该注意对比度，让文字对访客来说是清晰易读的。如果指定了一个图像，并且文本将被放置在该图像的顶部，还应该指定一个`background-color` ，以便在图像未加载时文本也足够清晰。

屏幕阅读器不能解析背景图像，因此它们应该是纯粹的装饰；任何重要的内容都应该是 HTML页面的一部分，而不是包含在背景中。









## 图像、视频和表单

图像和视频被描述为**[替换元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element)**。 这意味着CSS不能影响这些元素的内部布局-仅影响它们在页面上于其他元素中的位置。



调整图像大小

max-width：允许图片尺寸上小于但不大于盒子。

object-fit

- cover：缩小图像，维持图像的比例
- contain：图像缩放到可以放到盒子里的大小。
- fill：让图像充满盒子，但是不会维持比例。





## 表格



## 组织 CSS 

这些方法论都是有着结构化的编写和组织 CSS 途径的 CSS 代码指南。典型地，与你为你的项目编写和优化每个选择器为自己定义的规则组相比，它们会倾向于产生更多的多余代码。

### SUITCSS

### OOCSS

面向对象的CSS（OOCSS）

### BEM

BEM（Block Element Modifier，块级元素修饰字符）。在 BEM 中，一个块，例如一个按钮、菜单或者标志，就是独立的实体。







### SMACSS

Jonathan Snook创造的[Scalable and Modular Architecture for CSS (SMACSS)](http://smacss.com/)



### Systematic CSS

### ACSS

Yahoo!创造的[Atomic CSS (ACSS)](https://acss.io/)

### ITCSS

Harry Roberts的[ITCSS](https://itcss.io/)


