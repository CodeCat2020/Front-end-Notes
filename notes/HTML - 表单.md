

# 概述

**HTML表单是什么？**

HTML 表单用于搜集不同类型的用户输入。

HTML表单是用户和 Web 站点或应用程序之间交互的主要内容之一。它们允许用户将数据发送到 Web 站点。大多数情况下，数据被发送到 Web 服务器，但是 Web 页面也可以自己拦截它并使用它。

HTML 表单是由一个或多个小部件组成的。这些小部件可以是文本字段(单行或多行)、选择框、按钮、复选框或单选按钮。





# `<form>` 元素

HTML 表单用于收集用户输入。所有 HTML 表单都以一个 `<form>` 元素开始。

 `<form>` 正式定义了一个表单，是一个容器元素，但它也支持一些特定的属性来配置表单的行为方式。它的所有属性都是可选的，但实践中最好至少要设置 `action` 属性和 `method` 属性。

下面是 `<form>` 属性的列表：

| 属性           | 描述                                                       |
| :------------- | :--------------------------------------------------------- |
| accept-charset | 规定在被提交表单中使用的字符集（默认：页面字符集）。       |
| **action**     | 规定向何处提交表单的地址（URL）（提交页面）。              |
| autocomplete   | 规定浏览器应该自动完成表单（默认：开启）。                 |
| enctype        | 被提交数据的编码（默认：url-encoded）。                    |
| **method**     | 提交表单时所用的 HTTP 方法，GET 或 POST，默认为 GET。      |
| name           | 规定识别表单的名称（对于 DOM 使用：document.forms.name）。 |
| novalidate     | 规定浏览器不验证表单。                                     |
| target         | 规定 action 属性中地址的目标（默认：_self）。              |

例子：

```html
<form action="action_page.php" method="GET" target="_blank" accept-charset="UTF-8"
ectype="application/x-www-form-urlencoded" autocomplete="off" novalidate>
.
form elements
 .
</form> 
```



## action 属性

*action 属性*定义在提交表单时执行的动作。如果省略，则 action 会被设置为当前页面。

向服务器提交表单的通常做法是使用提交按钮。通常，表单会被提交到 web 服务器上的网页。

在上面的例子中，指定了某个服务器脚本来处理被提交表单：

```html
<form action="action_page.php">
```



## method 属性

*method 属性*规定在提交表单时所用的 HTTP 方法（*GET* 或 *POST*），默认为 GET。

```HTML
<form action="action_page.php" method="GET">
```

 GET 和 POST 的区别：

- 当表单被动提交（比如搜索引擎查询），并且没有敏感信息，使用 GET，表单数据在页面地址栏中是可见的。GET 最适合少量数据的提交。浏览器会设定容量限制。

  ```
  action_page.php?firstname=Mickey&lastname=Mouse
  ```

- 如果表单正在更新数据，或者包含敏感信息（例如密码），使用 POST，表单数据在页面地址栏中是不可见的。

method 属性可以被 `<button>` 、`<input type="submit">` 或 `<input type="image">` 元素中的 `formmethod` 属性覆盖。



表单提交中 GET 和 POST 方式的区别？

- get 是从服务器上获取数据， post 是向服务器传送数据。
- get 是把参数数据队列加到提交表单的 ACTION 属性所指的 URL 中，值和表单内各个字段一一对应，在 URL 中可以看到。 post 是通过 HTTP post 机制，将表单内各个字段与其内容放置在 HTML HEADER 内一起传送到 ACTION 属性所指的 URL 地址 , 用户看不到这个过程。
- 对于 get 方式，服务器端用 Request.QueryString 获取变量的值，对于 post 方式，服务器端用 Request.Form 获取提交的数据。
- get 传送的数据量较小，不能大于 2KB 。 post 传送的数据量较大，一般被默认为不受限制。但理论上， IIS4 中最大量为 80KB ， IIS5 中为 100KB 。
- get 安全性低， post 安全性较高。



## enctype 属性

当 `method` 属性值为 `post` 时，enctype 就是将表单的内容提交给服务器的 MIME 类型。可能的取值有：

- `application/x-www-form-urlencoded`：未指定属性时的默认值。
- **`multipart/form-data`** ：用于 `type ="file"` 的 `<input>` 元素。
- `text/plain`：(HTML5)

此值可以被 `<button>` 或者 `<input>` 元素中的 `formenctype` 属性覆盖。





# 表单元素

HTML 表单包含*表单元素*。表单本身并不可见，可见的是表单元素。



## `<input>` 元素

`<input>` 元素是最重要的表单元素，定义输入域。`<input>` 的属性如下：

| 属性                                                         | 值                                                           | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [accept](https://www.runoob.com/tags/att-input-accept.html)  | audio/* video/* image/* *MIME_type*                          | 规定通过文件上传来提交的文件的类型。 (只针对type="file")     |
| [align](https://www.runoob.com/tags/att-input-align.html)    | left right top middle bottom                                 | HTML5已废弃，不赞成使用。规定图像输入的对齐方式。 (只针对type="image") |
| [alt](https://www.runoob.com/tags/att-input-alt.html)        | *text*                                                       | 定义图像输入的替代文本。 (只针对type="image")                |
| [autocomplete](https://www.runoob.com/tags/att-input-autocomplete.html)（**New**） | on off                                                       | autocomplete 属性规定 <input> 元素输入字段是否应该启用自动完成功能。 |
| **autofocus**（**New**）                                     | autofocus                                                    | 属性规定当页面加载时 `<input>` 元素应该自动获得焦点。        |
| [checked](https://www.runoob.com/tags/att-input-checked.html) | checked                                                      | checked 属性规定在页面加载时应该被预先选定的 <input> 元素。 (只针对 type="checkbox" 或者 type="radio") |
| **disabled**                                                 | disabled                                                     | 规定应该禁用的 `<input>` 元素。无法修改内容，不会提交。      |
| [form](https://www.runoob.com/tags/att-input-form.html)（**New**） | *form_id*                                                    | form 属性规定 <input> 元素所属的一个或多个表单。             |
| [formaction](https://www.runoob.com/tags/att-input-formaction.html)（**New**） | *URL*                                                        | 属性规定当表单提交时处理输入控件的文件的 URL。(只针对 type="submit" 和 type="image") |
| [formenctype](https://www.runoob.com/tags/att-input-formenctype.html)（**New**） | application/x-www-form-urlencoded multipart/form-data text/plain | 属性规定当表单数据提交到服务器时如何编码(只适合 type="submit" 和 type="image")。 |
| [formmethod](https://www.runoob.com/tags/att-input-formmethod.html)（**New**） | get post                                                     | 定义发送表单数据到 action URL 的 HTTP 方法。 (只适合 type="submit" 和 type="image") |
| [formnovalidate](https://www.runoob.com/tags/att-input-formnovalidate.html)（**New**） | formnovalidate                                               | formnovalidate 属性覆盖 <form> 元素的 novalidate 属性。      |
| [formtarget](https://www.runoob.com/tags/att-input-formtarget.html)（**New**） | _blank _self _parent _top *framename*                        | 规定表示提交表单后在哪里显示接收到响应的名称或关键词。(只适合 type="submit" 和 type="image") |
| [height](https://www.runoob.com/tags/att-input-height.html)（**New**） | *pixels*                                                     | 规定 <input>元素的高度。(只针对type="image")                 |
| [list](https://www.runoob.com/tags/att-input-list.html)（**New**） | *datalist_id*                                                | 属性引用 <datalist> 元素，其中包含 <input> 元素的预定义选项。 |
| [max](https://www.runoob.com/tags/att-input-max.html)（**New**） | *number date*                                                | 属性规定 <input> 元素的最大值。                              |
| **maxlength**                                                | *number*                                                     | 属性规定 `<input>` 元素中允许的最大字符数。                  |
| [min](https://www.runoob.com/tags/att-input-min.html)（**New**） | *number date*                                                | 属性规定 <input>元素的最小值。                               |
| **multiple**（**New**）                                      | multiple                                                     | 属性规定允许用户输入到 `<input>` 元素的**多个值**。          |
| [name](https://www.runoob.com/tags/att-input-name.html)      | *text*                                                       | name 属性规定 <input> 元素的名称。                           |
| [pattern](https://www.runoob.com/tags/att-input-pattern.html)（**New**） | *regexp*                                                     | pattern 属性规定用于验证 <input> 元素的值的正则表达式。      |
| **placeholder**（**New**）                                   | *text*                                                       | placeholder 属性规定可描述输入 `<input>` 字段预期值的简短的**提示信息** 。 |
| **readonly**                                                 | readonly                                                     | 规定输入字段是**只读**的。<u>可以通过 JS 修改，内容会被提交</u>。能获得焦点。 |
| [required](https://www.runoob.com/tags/att-input-required.html)（**New**） | required                                                     | 属性规定必需在提交表单之前填写输入字段。                     |
| [size](https://www.runoob.com/tags/att-input-size.html)      | *number*                                                     | size 属性规定以字符数计的 <input> 元素的可见宽度。           |
| [src](https://www.runoob.com/tags/att-input-src.html)        | *URL*                                                        | src 属性规定显示为提交按钮的图像的 URL。 (只针对 type="image") |
| **step**（**New**）                                          | *number*                                                     | 规定 `<input>` 元素的合法数字间隔。不可以为负值或 0。        |
| [value](https://www.runoob.com/tags/att-input-value.html)    | *text*                                                       | 指定 <input> 元素 value 的值。                               |
| [width](https://www.runoob.com/tags/att-input-width.html)（**New**） | *pixels*                                                     | width 属性规定 <input> 元素的宽度。 (只针对type="image")     |

> 注意：
>
> MDN 说明 step 可以是任意字符串或是正浮点数。但是经过试验，step 为负数或 0 时会变成 1。 
>
> step 属性可以配合 max，min 属性来创建合法值得范围，适用于 input 类型有：number，range，date，datetime，month，time，week。



###  type 属性

根据不同的 *type* 属性，`<input>` 元素有很多形态。type 属性的取值可以是：

| Type                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **`button`**                                                 | 定义可点击的按钮（通常与 JavaScript 一起使用来启动脚本）。   |
| **`checkbox`**                                               | 复选框，从若干给定的选择中选取一个或若干选项。               |
| [color](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/color) | 用于指定颜色的控件；在支持的浏览器中，激活时会打开取色器。   |
| **`date`**（HTML5）                                          | 输入日期的控件（年、月、日，不包括时间）。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。 |
| [datetime-local](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/datetime-local) | 输入日期和时间的控件，不包括时区。在支持的浏览器激活时打开日期选择器或年月日的数字滚轮。 |
| [email](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/email) | 编辑邮箱地址的区域。类似 `text` 输入，但在支持的浏览器和带有动态键盘的设备上会有确认参数和相应的键盘。 |
| [file](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/file) | 让用户选择文件的控件。使用[accept](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#accept)属性规定控件能选择的文件类型。 |
| [hidden](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/hidden) | 不显示的控件，其值仍会提交到服务器。举个例子，右边就是一个隐形的控件。 |
| **`image`**                                                  | 带图像的 `submit` 按钮。显示的图像由 `src` 属性规定。如果 [src](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#src) 缺失，[alt](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#alt) 属性就会显示。 |
| [month](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/month) | 输入年和月的控件，没有时区。                                 |
| [number](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/number) | 用于输入数字的控件。如果支持的话，会显示滚动按钮并提供缺省验证（即只能输入数字）。拥有动态键盘的设备上会显示数字键盘。 |
| password                                                     | 密码字段。单行的文本区域，其值会被遮盖。如果站点不安全，会警告用户。 |
| radio                                                        | 单选按钮，允许在多个拥有相同 name 值的选项中选中其中一个。   |
| [range](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/range) | 此控件用于输入不需要精确的数字。控件是一个范围组件，默认值为正中间的值。同时使用[htmlattrdefmin](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#htmlattrdefmin)  和 [htmlattrdefmax](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input#htmlattrdefmax)来规定值的范围。 |
| [reset](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/reset) | 此按钮将表单的所有内容重置为默认值。不推荐。                 |
| [search](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/search) | 用于搜索字符串的单行文字区域。输入文本中的换行会被自动去除。在支持的浏览器中可能有一个删除按钮，用于清除整个区域。拥有动态键盘的设备上的回车图标会变成搜索图标。 |
| **`submit`**                                                 | 用于提交表单的按钮。                                         |
| [tel](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/tel) | 用于输入电话号码的控件。拥有动态键盘的设备上会显示电话数字键盘。 |
| text                                                         | 默认值。单行的文本区域，输入中的换行会被自动去除。默认宽度是 20 个字符 |
| [time](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/time) | 用于输入时间的控件，不包括时区。                             |
| [url](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/url) | 用于输入 URL 的控件。类似 `text` 输入，但有验证参数，在支持动态键盘的设备上有相应的键盘。 |
| [week](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/week) | 用于输入以年和周数组成的日期，不带时区。                     |
| **废弃的值**                                                 |                                                              |
| [datetime](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/datetime) | 用于输入基于UTC时区的日期和时间（时、分、秒及秒的小数部分）。 |



`date` 和 `datetime-local` 都可以用来绘制日历，样式可以通过 CSS 进行修改，目前来看支持opera 和 Chrome。https://www.w3school.com.cn/html5/html_5_form_input_types.asp

`datetime-local` 可以显示本地时间，且**可以修改**。



例子：

```html
<form>
    <!--常规文本字段 text-->
	 First name:<br>
	<input type="text" name="firstname">
	<br>
	 Last name:<br>
	<input type="text" name="lastname">
    <br>
    <!--密码字段 password-->
     PassWord:<br>
    <input type="password" name="password">
    
    <!--单选框 radio-->
    <br><br>
    <input type="radio" name="sex" value="male" checked>Male
	<br>
	<input type="radio" name="sex" value="female">Female
    
    <!--提交按钮 submit-->
	<br><br>
	<input type="submit" value="Submit">
</form> 
```

<form>
    <!--文本字段 text-->
	 First name:<br>
	<input type="text" name="firstname">
	<br>
	 Last name:<br>
	<input type="text" name="lastname">
    <br>
     PassWord:<br>
    <input type="password" name="pw">
    <!--单选框 radio-->
    <br><br>
	<input type="radio" name="sex" value="male" checked>Male
	<br>
	<input type="radio" name="sex" value="female">Female
	<!--提交按钮 submit-->
	<br><br>
	<input type="submit" value="Submit">
</form> 




### name 属性

如果要正确地被提交，每个输入字段必须设置一个 name 属性。

本例只会提交 " Last name" 输入字段：

```html
<form action="action_page.php">
	First name:<br>
	<input type="text" value="Mickey">
	<br>
	Last name:<br>
	<input type="text" name="lastname" value="Mouse">
	<br><br>
	<input type="submit" value="Submit">
</form> 
```



表单中的 input，id 和 name 的区别？

> https://www.cnblogs.com/dcc201108/p/4774110.html

- id ~ 身份证号码，name ~ 名字。id 显然是唯一的，而 name 是可以重复的。

- id 要符合标识的要求，比如大小写敏感，最好不要包含下划线（不兼容 CSS）。而 name 基本上没有什么要求，甚至可以用数字。

- id 是任何一个 HTML 元素都会有的，name 主要是表单元素里才有的属性。

  ```js
  document.表单名称.文本框.value		// 通过 name 获取元素
  document.getElementById("id")	// 通过 id 获取 非表单元素
  ```

- name 在以下用途是不能替代的

  - 表单(form)的控件名，提交的数据都用控件的 name 而不是 id 来控制。
  - frame 和 window 的名字，用于在其他 frame 或 window 指定 target。

- 两者都可以在锚点中使用，但是强烈建议用 id 不要用 name

  ```html
  <a name="myname">		<!-- 以前的写法 -->
  <div id="myid">			<!-- 现在可以用任何的元素 id 来指定 -->
  ```

- 以下情况只能用 id

  - label 与 form 控件的关联

    ```html
    <label for="MyInput">My Input</label>
    <input id="MyInput" type="text">
    ```

  - CSS 的元素选择机制，以 `#MyId` 的方式指定应用样式的元素，不能用name 替代。

  - 脚本中获得对象



## `<label>` 元素

 `<label>` 表示用户界面中某个元素的说明，定义表单控制间的关系。当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

| 属性            | 值           | 描述                                  |
| :-------------- | :----------- | :------------------------------------ |
| for             | *element_id* | 规定 label 与哪个表单元素绑定。       |
| form（**New**） | *form_id*    | 规定 label 字段所属的一个或多个表单。 |

label 只有两个属性 for 和 form，没有 id 属性。错误例子：

```
<label id="mylabel"></label>
```

 `<label>` 用法：

将一个 `<label>` 和一个 `<input>` 元素匹配在一起，需要给 `<input>` 一个 `id` 属性，`<label>` 一个 `for` 属性，两者的值一样。

```html
<label for="cheese">Do you like cheese?</label>
<input type="checkbox" name="cheese" id="cheese">
```

也可以将 `<input>` 直接放在 `<label>` 里，此时不需要 `for` 和 `id` 属性，因为关联是隐含的：

```html
<label>Do you like peas?
  <input type="checkbox" name="peas">
</label>
```





##  `<fieldset>` 元素

 `<fieldset>`  元素组合表单中的相关数据。 `<legend>` 元素为 `<fieldset>` 元素定义标题。

```html
<fieldset><br /><legend>类型名</legend><br />内容显示<br /></fieldset>
```

fieldset 用来分组，而 legend 用来分组描述。

```html
<form action="action_page.php">
	<fieldset>
		<!-- legend 元素为 fieldset 元素定义标题。-->
		<legend>Personal information:</legend>

		First name:<br>
		<input type="text" name="firstname" value="Mickey">
		<br>
		Last name:<br>
		<input type="text" name="lastname" value="Mouse">
		<br><br>
		<input type="submit" value="Submit">
    </fieldset>
</form> 
```

<form action="action_page.php">
	<fieldset>
	<legend>Personal information:</legend>
	First name:<br>
	<input type="text" name="firstname" value="Mickey">
	<br>
	Last name:<br>
	<input type="text" name="lastname" value="Mouse">
	<br><br>
	<input type="submit" value="Submit">
    </fieldset>
</form>



## `<button>` 元素

button 元素可以嵌套没有 control 属性的 video 元素。





# 总结

层次显示优先级：

在 HTML 中，帧元素（frameset）的优先级最高，表单元素比非表单元素的优先级要高。

- 表单元素包括：文本输入框，密码输入框，单选框，复选框，文本输入域，列表框等等。
- 非表单元素包括：a，div，table，span等。

所有的 HTML 元素又可以根据其显示分成两类：有窗口元素以及无窗口元素。有窗口元素总是显示在无窗口元素的前面。

- 有窗口元素包括：select元素，object元素，以及frames元素等等。

- 无窗口元素：大部分html元素都是无窗口元素。


层级显示优先级： frameset > 表单元素 > 非表单元素
