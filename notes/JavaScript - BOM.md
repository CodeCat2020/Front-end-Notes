

# BOM



浏览器对象模型（BOM，Browser Object Model）以 window 对象为依托，表示浏览器窗口以及页面可见区域。

BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关。W3C 为了把浏览器中 JavaScript 最基本的部分标准化，已经将 BOM 的主要方面纳入了 HTML5 的规范中。





BOM 是浏览器对象。常用的 BOM 属性：

- Window 对象表示浏览器中打开的窗口
- Location 对象包含有关当前 URL 的信息
- Navigator 对象包含有关浏览器的信息
- History 对象包含用户（在浏览器窗口中）访问过的 URL







## 1. Window 对象

BOM 的核心对象是 window，它表示浏览器的一个实例，表示浏览器中打开的窗口，可用于检索有关窗口状态的信息。

- window 对象是浏览器所有内容的主容器。
- 浏览器打开 HTML 文档时，通常会创建一个 window 对象。





### 全局作用域

在浏览器中，window 对象有双重角色，它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。因而所有全局变量和函数都是它的属性，且所有原生的构造函数及其他函数也都存在于它的命名空间下。

```js
var age = 29;
function sayAge(){
    alert(this.age);
}
alert(window.age); 	// 29
sayAge(); 			// 29
window.sayAge(); 	// 29
```

定义全局变量与在 window 对象上直接定义属性的差别：全局变量不能通过 delete 操作符删除，而直接在 window 对象上的定义的属性可以。

使用 var 语句添加的 window 属性有一个名为 [[Configurable]] 的特性，这个特性的值被设置为 false，因此这样定义的属性不可以通过 delete 操作符删除。IE8 及更早版本在遇到使用 delete 删除 window 属性的语句时，不管该属性最初是如何创建的，都会抛出错误，以示警告。IE9 及更高版本不会抛出错误。

```js
var age = 29;				// 全局变量
window.color = "red";		// 在 window 对象上直接定义属性
// 在IE < 9 时抛出错误，在其他所有浏览器中都返回 false
delete window.age;			
// 在IE < 9 时抛出错误，在其他所有浏览器中都返回 true
delete window.color; 		// returns true
alert(window.age); 			// 29
alert(window.color); 		// undefined
```

尝试访问未声明的变量会抛出错误，但是通过查询 window 对象，可以知道某个可能未声明的变量是否存在。

```js
var newValue = oldValue;		// 抛出错误，因为 oldValue 未定义
var newValue = window.oldValue;	// 不会抛出错误，因为这是一次属性查询，newValue 的值是 undefined
```



### 窗口关系及框架 

**frames**

如果页面中包含框架，则每个框架都拥有自己的 window 对象以及所有原生构造函数及其他函数的副本。每个框架都保存在 frames 集合中。

在 frames 集合中，可以通过数值索引（从0 开始，从左至右，从上到下）或者框架名称来访问相应的 window 对象。每个 window 对象都有一个 name 属性，其中包含框架的名称。

有一些窗口指针，可以用来引用其他框架，包括父框架。





**top**

top 对象始终指向最高（最外）层的框架，也就是浏览器窗口。使用它可以确保在一个框架中正确地访问另一个框架。因为对于在一个框架中编写的任何代码来说，其中的 window 对象指向的都是那个框架的特定实例，而非最高层的框架。

**parent**

与 top 相对的另一个 window 对象是 parent。顾名思义，parent（父）对象始终指向当前框架的直接上层框架。在某些情况下，parent 有可能等于 top；但在没有框架的情况下，parent  一定等于 top（此时它们都等于window）。



**self**

self 始终指向 window；实际上，self 和 window 对象可以互换使用。引入 self 对象的目的只是为了与 top 和parent 对象对应起来，因此它不格外包含其他值。

所有这些对象都是 window 对象的属性，可以通过 window.parent、window.top 等形式来访问。同时，这也意味着可以将不同层次的 window 对象连缀起来，例如 window.parent.parent.frames[0]。







### 窗口位置

用来确定和修改 window 对象位置的属性和方法有很多。

IE、Safari、Opera 和 Chrome 都提供了 screenLeft 和 screenTop 属性，分别用于表示窗口相对于屏幕左边和上边的位置。

Firefox 则在 screenX 和 screenY 属性中提供相同的窗口位置信息，Safari 和 Chrome 也同时支持这两个属性。Opera 虽然也支持 screenX 和 screenY 属性，但与 screenLeft 和 screenTop 属性并不对应，因此建议大家不要在 Opera 中使用它们。使用下列代码可以跨浏览器取得窗口左边和上边的位置。

```js
var leftPos = (typeof window.screenLeft == "number") ?
window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ?
window.screenTop : window.screenY;
```



使用 moveTo() 和 moveBy() 方法有可能将窗口精确地移动到一个新位置。这两个方法都接收两个参数，其中 moveTo() 接收的是新位置的 x 和 y 坐标值，而 moveBy() 接收的是在水平和垂直方向上移动的像素数。



**screenLeft**



**screenTop**





**moveTo()**

**moveBy()**





### 窗口大小

**innerWidth**

**innerHeight**

**outerWidth** 

**outerHeight**



### 导航和打开窗口

#### open()

使用 window.open() 方法可以导航到一个特定的 URL，也可以打开一个新的浏览器窗口。

```
window.open(URL,name,specs,replace)
```

| 参数    | 说明                                                         |
| :------ | :----------------------------------------------------------- |
| URL     | 可选。打开指定的页面的 URL。如果没有，打开一个新的空白窗口。 |
| name    | 可选。指定 target 属性或窗口的名称。                         |
| specs   | 可选。一个逗号分隔的项目列表。                               |
| replace | Optional.Specifies规定了装载到窗口的 URL 是在窗口的浏览历史中创建一个新条目，还是替换浏览历史中的当前条目。支持下面的值：true - URL 替换浏览历史中的当前条目。false - URL 在浏览历史中创建新的条目。 |





### 间歇调用和超时调用

JavaScript 是单线程语言，但它允许通过设置超时值和间歇时间值来调度代码在特定的时刻执行。

####  **setTimeout() **

超时调用需要使用 window 对象的 setTimeout() 方法。

它接受两个参数：要执行的代码和以毫秒表示的时间（即在执行代码前需要等待多少毫秒）。其中，第一个参数可以是一个包含 JavaScript 代码的字符串，也可以是一个函数。

```js
// 可能导致性能损失，不建议传递字符串！
setTimeout("alert('Hello world!') ", 1000);
// 推荐的调用方式
setTimeout(function() {
	alert("Hello world!");
}, 1000);
```

####  clearTimeout()

调用 setTimeout() 之后，该方法会返回一个数值 ID，表示超时调用。这个超时调用 ID 是计划执行代码的唯一标识符，可以通过它来取消超时调用。要取消尚未执行的超时调用计划，可以调用 clearTimeout() 方法并将相应的超时调用 ID 作为参数传递给它。只要是在指定的时间尚未过去之前调用 clearTimeout()，就可以完全取消超时调用。

```js
//设置超时调用
var timeoutId = setTimeout(function() {alert("Hello world!");}, 1000);
//注意：把它取消
clearTimeout(timeoutId);
```



####  **setInterval()**

间歇调用与超时调用类似，只不过它会按照指定的时间间隔重复执行代码，直至间歇调用被取消或者页面被卸载。设置间歇调用的方法是 setInterval()，参数与 setTimeout() 相同。

```js
//不建议传递字符串！
setInterval ("alert('Hello world!') ", 10000);
//推荐的调用方式
setInterval (function() {alert("Hello world!");}, 10000);
```

####  clearInterval()

调用 setInterval() 方法同样也会返回一个间歇调用ID，该 ID 可用于在将来某个时刻取消间歇调用。要取消尚未执行的间歇调用，可以使用 clearInterval() 方法并传入相应的间歇调用 ID。取消间歇调用的重要性要远远高于取消超时调用，因为在不加干涉的情况下，间歇调用将会一直执行到页面卸载。

```js
var num = 0;
var max = 10;
var intervalId = null;
function incrementNumber() {
    num++;
    //如果执行次数达到了max 设定的值，则取消后续尚未执行的调用
    if (num == max) {
    	clearInterval(intervalId);
    	alert("Done");
	}
}
intervalId = setInterval(incrementNumber, 500);
```







### 系统对话框

浏览器通过 alert()、confirm() 和 prompt() 方法可以调用系统对话框向用户显示消息。



**alert()**

**confirm()**

**prompt()**



### 小结

#### 属性

window 对象属性

| 属性                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [closed](https://www.runoob.com/jsref/prop-win-closed.html)  | 返回窗口是否已被关闭。                                       |
| [defaultStatus](https://www.runoob.com/jsref/prop-win-defaultstatus.html) | 设置或返回窗口状态栏中的默认文本。                           |
| [document](https://www.runoob.com/jsref/dom-obj-document.html) | 对 Document 对象的只读引用。(请参阅[对象](https://www.runoob.com/jsref/dom-obj-document.html)) |
| **frames**                                                   | 返回窗口中所有命名的框架。该集合是 Window 对象的数组，每个 Window 对象在窗口中含有一个框架。 |
| **history**                                                  | 对 History 对象的只读引用。请参数 [History 对象](https://www.runoob.com/jsref/obj-history.html)。 |
| [innerHeight](https://www.runoob.com/jsref/prop-win-innerheight.html) | 返回窗口的文档显示区的高度。                                 |
| [innerWidth](https://www.runoob.com/jsref/prop-win-innerheight.html) | 返回窗口的文档显示区的宽度。                                 |
| [localStorage](https://www.runoob.com/jsref/prop-win-localstorage.html) | 在浏览器中存储 key/value 对。没有过期时间。                  |
| [length](https://www.runoob.com/jsref/prop-win-length.html)  | 设置或返回窗口中的框架数量。                                 |
| **location**                                                 | 用于窗口或框架的 Location 对象。请参阅 [Location 对象](https://www.runoob.com/jsref/obj-location.html)。 |
| [name](https://www.runoob.com/jsref/prop-win-name.html)      | 设置或返回窗口的名称。                                       |
| **navigator**                                                | 对 Navigator 对象的只读引用。请参数 [Navigator 对象](https://www.runoob.com/jsref/obj-navigator.html)。 |
| [opener](https://www.runoob.com/jsref/prop-win-opener.html)  | 返回对创建此窗口的窗口的引用。                               |
| [outerHeight](https://www.runoob.com/jsref/prop-win-outerheight.html) | 返回窗口的外部高度，包含工具条与滚动条。                     |
| [outerWidth](https://www.runoob.com/jsref/prop-win-outerheight.html) | 返回窗口的外部宽度，包含工具条与滚动条。                     |
| [pageXOffset](https://www.runoob.com/jsref/prop-win-pagexoffset.html) | 设置或返回当前页面相对于窗口显示区左上角的 X 位置。          |
| [pageYOffset](https://www.runoob.com/jsref/prop-win-pagexoffset.html) | 设置或返回当前页面相对于窗口显示区左上角的 Y 位置。          |
| **parent**                                                   | 返回父窗口。                                                 |
| **screen**                                                   | 对 Screen 对象的只读引用。请参数 [Screen 对象](https://www.runoob.com/jsref/obj-screen.html)。 |
| screenLeft                                                   | 返回相对于屏幕窗口的x坐标                                    |
| screenTop                                                    | 返回相对于屏幕窗口的y坐标                                    |
| [screenX](https://www.runoob.com/jsref/prop-win-screenx.html) | 返回相对于屏幕窗口的x坐标                                    |
| [sessionStorage](https://www.runoob.com/jsref/prop-win-sessionstorage.html) | 在浏览器中存储 key/value 对。 在关闭窗口或标签页之后将会删除这些数据。 |
| [screenY](https://www.runoob.com/jsref/prop-win-screenx.html) | 返回相对于屏幕窗口的y坐标                                    |
| **self**                                                     | 返回对当前窗口的引用。等价于 Window 属性。                   |
| [status](https://www.runoob.com/jsref/prop-win-status.html)  | 设置窗口状态栏的文本。                                       |
| **top**                                                      | 返回最顶层的父窗口。                                         |





#### 方法

window 对象方法

| 方法                                                         | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| **alert()**                                                  | 显示带有一段消息和一个确认按钮的警告框。                     |
| [atob()](https://www.runoob.com/jsref/met-win-atob.html)     | 解码一个 base-64 编码的字符串。                              |
| [btoa()](https://www.runoob.com/jsref/met-win-btoa.html)     | 创建一个 base-64 编码的字符串。                              |
| [blur()](https://www.runoob.com/jsref/met-win-blur.html)     | 把键盘焦点从顶层窗口移开。                                   |
| **clearInterval()**                                          | 取消由 setInterval() 设置的 timeout。                        |
| **clearTimeout()**                                           | 取消由 setTimeout() 方法设置的 timeout。                     |
| [close()](https://www.runoob.com/jsref/met-win-close.html)   | 关闭浏览器窗口。                                             |
| **confirm()**                                                | 显示带有一段消息以及确认按钮和取消按钮的对话框。             |
| [createPopup()](https://www.runoob.com/jsref/met-win-createpopup.html) | 创建一个 pop-up 窗口。                                       |
| [focus()](https://www.runoob.com/jsref/met-win-focus.html)   | 把键盘焦点给予一个窗口。                                     |
| getSelection()                                               | 返回一个 Selection 对象，表示用户选择的文本范围或光标的当前位置。 |
| [getComputedStyle()](https://www.runoob.com/jsref/jsref-getcomputedstyle.html) | 获取指定元素的 CSS 样式。                                    |
| [matchMedia()](https://www.runoob.com/jsref/met-win-matchmedia.html) | 该方法用来检查 media query 语句，它返回一个 MediaQueryList对象。 |
| **moveBy()**                                                 | 可相对窗口的当前坐标把它移动指定的像素。                     |
| **moveTo()**                                                 | 把窗口的左上角移动到一个指定的坐标。                         |
| **open()**                                                   | 打开一个新的浏览器窗口或查找一个已命名的窗口。               |
| [print()](https://www.runoob.com/jsref/met-win-print.html)   | 打印当前窗口的内容。                                         |
| **prompt()**                                                 | 显示可提示用户输入的对话框。                                 |
| [resizeBy()](https://www.runoob.com/jsref/met-win-resizeby.html) | 按照指定的像素调整窗口的大小。                               |
| [resizeTo()](https://www.runoob.com/jsref/met-win-resizeto.html) | 把窗口的大小调整到指定的宽度和高度。                         |
| scroll()                                                     | 已废弃。 该方法已经使用了 [scrollTo()](https://www.runoob.com/jsref/met-win-scrollto.html) 方法来替代。 |
| scrollBy()                                                   | 按照指定的像素值来滚动内容。                                 |
| scrollTo()                                                   | 把内容滚动到指定的坐标。                                     |
| **setInterval()**                                            | 按照指定的周期（以毫秒计）来调用函数或计算表达式。           |
| **setTimeout()**                                             | 在指定的毫秒数后调用函数或计算表达式。                       |
| [stop()](https://www.runoob.com/jsref/met-win-stop.html)     | 停止页面载入。                                               |













## 2. location 对象

location 对象提供了与当前窗口中加载的文档有关的信息和一些导航功能。<u>location 对象包含有关当前 URL 的信息</u>。





-  使用 location 对象可以通过编程方式来访问浏览器的导航系统。设置相应的属性，可以逐段或整体性地修改浏览器的URL。



location 对象既是 window 对象的属性，也是 document 对象的属性，window.location 和 document.location 引用的是同一个对象。

location 用于获取或设置窗体的 URL。location 对象的用处还表现在它将 URL 解析为独立的片段，让开发人员可以通过不同的属性访问这些片段。

下表列出了location 对象的所有属性（注：省略了每个属性前面的 location 前缀）。

**location 对象属性**

| 属性                                                         | 描述                          |
| :----------------------------------------------------------- | :---------------------------- |
| [hash](https://www.runoob.com/jsref/prop-loc-hash.html)      | 返回一个URL的锚部分           |
| [host](https://www.runoob.com/jsref/prop-loc-host.html)      | 返回一个URL的主机名和端口     |
| [hostname](https://www.runoob.com/jsref/prop-loc-hostname.html) | 返回URL的主机名               |
| [href](https://www.runoob.com/jsref/prop-loc-href.html)      | 返回完整的URL                 |
| [pathname](https://www.runoob.com/jsref/prop-loc-pathname.html) | 返回的URL路径名。             |
| [port](https://www.runoob.com/jsref/prop-loc-port.html)      | 返回一个URL服务器使用的端口号 |
| [protocol](https://www.runoob.com/jsref/prop-loc-protocol.html) | 返回一个URL协议               |
| **search**                                                   | 返回一个URL的查询部分         |

**location 对象方法**

| 方法                                                         | 说明                   |
| :----------------------------------------------------------- | :--------------------- |
| **assign()**                                                 | 载入一个新的文档       |
| [reload()](https://www.runoob.com/jsref/met-loc-reload.html) | 重新载入当前文档       |
| [replace()](https://www.runoob.com/jsref/met-loc-replace.html) | 用新的文档替换当前文档 |





### 查询字符串参数 search

### 位置操作 assign()

 调用replace()方法可以导航到一个新URL，同时该URL 会替换浏览器历史记录中当前显示的页面。



## 3. navigator 对象

Navigator 对象<u>包含有关浏览器的信息</u>，通常用于检测浏览器与操作系统的版本。

到底提供哪些信息，很大程度上取决于用户的浏览器；不过，也有一些公共的属性（如userAgent）存在于所有浏览器中。



**navigator 对象属性**

| 属性                                                         | 说明                                         |
| :----------------------------------------------------------- | :------------------------------------------- |
| [appCodeName](https://www.runoob.com/jsref/prop-nav-appcodename.html) | 返回浏览器的代码名                           |
| [appName](https://www.runoob.com/jsref/prop-nav-appname.html) | 返回浏览器的名称                             |
| [appVersion](https://www.runoob.com/jsref/prop-nav-appversion.html) | 返回浏览器的平台和版本信息                   |
| [cookieEnabled](https://www.runoob.com/jsref/prop-nav-cookieenabled.html) | 返回指明浏览器中是否启用 cookie 的布尔值     |
| [platform](https://www.runoob.com/jsref/prop-nav-platform.html) | 返回运行浏览器的操作系统平台                 |
| **plugins**                                                  | 浏览器中安装的插件信息的数组                 |
| [userAgent](https://www.runoob.com/jsref/prop-nav-useragent.html) | 返回由客户机发送服务器的 user-agent 头部的值 |



userAgent 属性是一个只读的字符串，声明了浏览器用于 HTTP 请求的用户代理头的值。



**navigator 对象方法**

| 方法                                                         | 描述                                      |
| :----------------------------------------------------------- | :---------------------------------------- |
| [javaEnabled()](https://www.runoob.com/jsref/met-nav-javaenabled.html) | 指定是否在浏览器中启用Java                |
| [taintEnabled()](https://www.runoob.com/jsref/met-nav-taintenabled.html) | 规定浏览器是否启用数据污点(data tainting) |











### 检测插件 plugins

对于非IE 浏览器，可以使用 plugins 数组来达到这个目的。该数组中的每一项都包含下列属性。

- name：插件的名字。
- description：插件的描述。
- filename：插件的文件名。
- length：插件所处理的 MIME 类型数量。





### 注册处理程序

#### registerContentHandler()

#### registerProtocolHandler()





## 4. screen 对象

screen 对象中保存着与客户端显示器有关的信息，这些信息一般只用于站点分析。每个浏览器中的 screen 对象都包含着各不相同的属性。

**screen 对象属性**

| 属性                                                         | 说明                                     |
| :----------------------------------------------------------- | :--------------------------------------- |
| [availHeight](https://www.runoob.com/jsref/prop-screen-availheight.html) | 返回屏幕的高度（不包括Windows任务栏）    |
| [availWidth](https://www.runoob.com/jsref/prop-screen-availwidth.html) | 返回屏幕的宽度（不包括Windows任务栏）    |
| [colorDepth](https://www.runoob.com/jsref/prop-screen-colordepth.html) | 返回目标设备或缓冲器上的调色板的比特深度 |
| [height](https://www.runoob.com/jsref/prop-screen-height.html) | 返回屏幕的总高度                         |
| [pixelDepth](https://www.runoob.com/jsref/prop-screen-pixeldepth.html) | 返回屏幕的颜色分辨率（每象素的位数）     |
| [width](https://www.runoob.com/jsref/prop-screen-width.html) | 返回屏幕的总宽度                         |



## 5. history 对象

history 对象保存着用户上网的历史记录，从窗口被打开的那一刻算起。

因为 history 是 window 对象的属性，因此每个浏览器窗口、每个标签页乃至每个框架，都有自己的 history 对象与特定的 window 对象关联。

出于安全方面的考虑，开发人员无法得知用户浏览过的 URL。不过，借由用户访问过的页面列表，开发人员可以判断历史记录的数量，也可以在历史记录中向后或向前导航到任意页面。

**history 对象属性**

| 属性       | 说明                     |
| :--------- | :----------------------- |
| **length** | 返回历史列表中的网址数。 |

**History 对象方法**

| 方法                                                 | 说明                              |
| :--------------------------------------------------- | :-------------------------------- |
| **back()**                                           | 加载 history 列表中的前一个 URL。 |
| **forward()**                                        | 加载 history 列表中的下一个 URL。 |
| [go()](https://www.runoob.com/jsref/met-his-go.html) | 加载 history 列表中的某个具体页面 |



 **go()**

使用 go() 方法可以在用户的历史记录中任意跳转。这个方法接受一个参数，表示跳转的页面数的一个整数值。负数表示向后跳转，正数表示向前跳转。

```js
// 后退一页
history.go(-1);
// 前进一页
history.go(1);
// 前进两页
history.go(2);
```

也可以给 go() 方法传递一个字符串参数，此时浏览器会跳转到历史记录中包含该字符串的第一个位置——可能后退，也可能前进，具体要看哪个位置最近。如果历史记录中不包含该字符串，那么这个方法什么也不做。

```js
history.go("wrox.com");			// 跳转到最近的 wrox.com 页面
history.go("nczonline.net");	// 跳转到最近的 nczonline.net 页面
```

**back()** 和 **forward()**

还可以使用两个简写方法 back() 和 forward() 来代替 go()。

```js
history.back();		// 后退一页
history.forward();	// 前进一页
```

 **length 属性**

history 对象的 length 属性，保存着历史记录的数量。这个数量包括所有历史记录，即所有向后和向前的记录。对于加载到窗口、标签页或框架中的第一个页面而言，history.length 等于0。

```js
if (history.length == 0){
	// 这应该是用户打开窗口后的第一个页面
}
```





