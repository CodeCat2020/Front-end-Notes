# Ajax

## 定义

Ajax（Asynchronous JavaScript and XML， 异步的 JavaScript 和 XML ）。

传统的网页如果需要更新内容，必须重新加载整个网页。使用 Ajax 无需刷新页面就能够从服务器取得数据。

Ajax 不是新的编程语言，而是一种用于创建动态网页的技术。通过与服务器进行少量数据交换， Ajax 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

支持 Ajax 的浏览器目前包括： Mozilla 、Firefox 、Internet Explorer 、Opera 、Konqueror 及 Safari 。但是 Opera 不支持 XSL 格式的对象，也不支持 XSLT。

Ajax 可以提高系统性能， 优化用户界面。很多框架以及代码库已将 Ajax 作为其必不可少的一个重要模块。











Ajax 的优点是什么？

- 不需要插件支持
- 最大的优点：页面无刷新更新，用户的体验非常好。
- 提高 Web 程序性能
- 减轻服务器和带宽的负担。可以将一些服务器工作转移到客户端，利用客户端资源来处理，减轻服务器和带宽的压力，节约空间和带宽租用成本。Ajax 的原则是“按需获取数据”，可以最大限度地减少冗余请求及响应对服务器造成的负担。
- 使用异步方式与服务器通信，具有更迅速的响应能力。
- 
- 技术标准化，并被浏览器广泛支持，不需要下载
- Ajax 对 CSS 、文本支持很好，支持搜索
- 开放性，易用性及易于开发。



Ajax 的缺点是什么？

- 有安全问题， Ajax 暴露了与服务器交互的细节。
- 破坏了程序的异常机制。
- 不适合处理多媒体、矢量图形、机器访问。
- 
- 浏览器对 XMLHTTPRequest 对象的支持度不足。
- <u>破坏浏览器前进、“后退”按钮的正常功能</u>。
- 对搜索引擎的支持的不足。
- 开发和调试工具的缺乏，不容易调试。





## XMLHttpRequest 对象



Ajax 技术的核心是 XMLHttpRequest 对象（简称 XHR）。XHR 对象由微软最早在 IE5 中引入，用于通过 JavaScript 从服务器取得 XML 数据。

在 IE5 中，XHR 对象是通过 MSXML 库中的一个 ActiveX 对象实现的。因此，在 IE 中可能会遇到三种不同版本的 XHR 对象，即 MSXML2.XMLHttp、MSXML2.XMLHttp.3.0 和 MXSML2.XMLHttp.6.0。

在此之后，Firefox、Safari、Chrome 和 Opera 都实现了相同的特性，使 XHR 成为了 Web 的一个事实标准。IE7+、Firefox、Opera、Chrome 和 Safari 都支持原生的 XHR 对象。

整个 XMLHttpRequest 对象的生命周期应该包含如下阶段： 创建－初始化请求－发送请求－接收数据－解析数据－完成。

### 创建 XHR 对象

在 IE7+ 中，使用 XMLHttpRequest 构造函数创建 XHR 对象。在 IE6 和 IE5 中，使用 ActiveXObject 构造函数创建 XHR 对象。

```js
var xhr;
if(window.XMLHttpRequest){
    // IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xhr = new XMLHttpRequest();
}else{
    // IE6, IE5 浏览器执行代码
    xhr = new ActiveXObject('Microsoft.XMLHTTP');
}
```



### XHR 的用法

**open() 初始化请求**

在使用 XHR 对象时，<u>要调用的第一个方法是 open()</u>，它不会真正发送请求，而是启动一个请求以备发送。

接受 3 个参数：

- *method*：请求的类型（"get"、"post"等）。
- *url*：请求的 URL（文件在服务器上的位置）。
- *async*：是否异步发送请求，true（异步）或 false（同步），默认 true。
  - 同步请求，JavaScript 代码会等到服务器响应之后再继续执行。
  - 异步请求，JavaScript 继续执行而不必等待响应。

```js
xhr.open("get", "example.txt", false);		// 启动一个请求以备发送。
```

注意：只能向同一个域中使用相同端口和协议的 URL 发送请求。如果 URL 与启动请求的页面有任何差别，都会引发安全错误。

**send() 发送请求**

发送特定的请求，必须调用 send() 方法。 send() 方法接收一个参数（必需），即要作为请求主体发送的数据。如果不需要通过请求主体发送数据，则必须传入 null。调用 send() 后，请求会被分派到服务器。

```js
xhr.send(null);
```



**与响应相关的属性**

在收到响应后，响应的数据会自动填充 XHR 对象的属性，相关的属性简介如下。

- responseText：作为响应主体被返回的文本。
- responseXML：如果响应的内容类型是"text/xml"或"application/xml"，这个属性中将保存包含着响应数据的 XML DOM 文档。
- status：响应的 HTTP 状态。
- statusText：HTTP 状态的说明。

在接收到响应后，第一步是检查 status 属性，以确定响应已经成功返回。一般来说，可以将 HTTP 状态代码为 200 作为成功的标志。此时，responseText 属性的内容已经就绪，而且在内容类型正确的情况下，responseXML 也能够访问了。此外，状态代码为 304 表示请求的资源并没有被修改，可以直接使用浏览器中缓存的版本；当然，也意味着响应是有效的。

为确保接收到适当的响应，应该像下面这样检查上述这两种状态代码：

```js
// 状态码是否是 2xx 或者 304
if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
    alert(xhr.responseText);
} else {
    alert("Request was unsuccessful: " + xhr.status);
}
```

建议通过检测 status 来决定下一步的操作，不要依赖 statusText，因为后者在跨浏览器使用时不太可靠。



 **readyState 属性**

XHR 对象的 readyState 属性表示请求/响应过程的当前活动阶段。这个属性可取的值如下。

- 0 `UNSENT`：未初始化。尚未调用 open() 方法。
- 1 `OPENED`：启动（服务器连接已建立）。已经调用 open() 方法，但尚未调用 send() 方法。
- 2 `HEADERS_RECEIVED`：发送（请求已接收）。已经调用 send() 方法，但尚未接收到响应。
- **3 `LOADING`：接收**（请求处理中）。已经接收到部分响应数据。
- **4 `DONE`：完成**（请求已完成，且响应已就绪）。已经接收到全部响应数据，而且已经可以在客户端使用了。

> 在IE中，状态有着不同的名称： `READYSTATE_UNINITIALIZED` (0)，`READYSTATE_LOADING` (1) ， `READYSTATE_LOADED` (2) ， `READYSTATE_INTERACTIVE` (3) 和 `READYSTATE_COMPLETE` (4) 。

只要 readyState 属性的值由一个值变成另一个值，都会触发一次 readystatechange 事件。可以利用这个事件来检测每次状态变化后 readyState 的值。通常，我们只对 readyState 值为 4 的阶段感兴趣，因为这时所有数据都已经就绪。

不过，必须在调用 open() 之前指定 onreadystatechange 事件处理程序才能确保跨浏览器兼容性。（为什么？）（？）



**abort() 取消异步请求**

在接收到响应前，可以调用 abort() 方法来取消异步请求。调用这个方法后，XHR 对象会停止触发事件，而且也不再允许访问任何与响应有关的对象属性。在终止请求之后，还应该对 XHR 对象进行解引用操作。由于内存原因，不建议重用 XHR 对象。

```js
xhr.abort();
```



**HTTP 头部信息**

每个 HTTP 请求和响应都会带有相应的头部信息，XHR 对象也提供了操作请求头部和响应头部信息的方法。

默认情况下，在发送 XHR 请求的同时，还会发送下列头部信息。

- Accept：浏览器能够处理的内容类型。
- Accept-Charset：浏览器能够显示的字符集。
- Accept-Encoding：浏览器能够处理的压缩编码。
- Accept-Language：浏览器当前设置的语言。
- Connection：浏览器与服务器之间连接的类型。
- Cookie：当前页面设置的任何Cookie。
- Host：发出请求的页面所在的域 。
- Referer：发出请求的页面的URI。注意，HTTP 规范将这个头部字段拼写错了，而为保证与规范一致，也只能将错就错了。（这个英文单词的正确拼法应该是referrer。）
- User-Agent：浏览器的用户代理字符串。

**setRequestHeader()**

使用 setRequestHeader() 方法可以设置自定义的请求头部信息。这个方法接受两个参数：头部字段的名称和头部字段的值。要成功发送请求头部信息，必须在调用 open() 方法之后且调用 send() 方法之前调用 setRequestHeader()。

 **getResponseHeader()、getAllResponseHeaders() **

调用 XHR 对象的 getResponseHeader() 方法并传入头部字段名称，可以取得相应的响应头部信息。而调用 getAllResponseHeaders() 方法则可以取得一个包含所有头部信息的长字符串。

```js
var xhr = createXHR();
xhr.onreadystatechange = function(){
    if (xhr.readyState == 4){
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            alert(xhr.responseText);
            var myHeader = xhr.getResponseHeader("MyHeader");
			var allHeaders = xhr.getAllResponseHeaders();
        } else {
            alert("Request was unsuccessful: " + xhr.status);
        }
    }
};
xhr.open("get", "example.php", true);
xhr.setRequestHeader("MyHeader", "MyValue");
xhr.send(null);
```



### GET 请求

使用 GET 请求经常会发生的一个错误，就是查询字符串的格式有问题。查询字符串中每个参数的名称和值都必须使用 encodeURIComponent() 进行编码，然后才能放到 URL 的末尾；而且所有名-值对儿都必须由和号（&）分隔，如下面的例子所示。

```js
xhr.open("get", "example.php?name1=value1&name2=value2", true);
```

下面这个函数可以辅助向现有 URL 的末尾添加查询字符串参数：

```js
function addURLParam(url, name, value) {
    url += (url.indexOf("?") == -1 ? "?" : "&");
    url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
    return url;
}
```



### POST 请求

在 open() 方法第一个参数的位置传入"post"，就可以初始化一个 POST 请求，如下面
的例子所示。

```js
xhr.open("post", "example.php", true);
```

发送 POST 请求的第二步就是向 send() 方法中传入某些数据。由于 XHR 最初的设计主要是为了处理 XML，因此可以在此传入 XML DOM 文档，传入的文档经序列化之后将作为请求主体被提交到服务器。当然，也可以在此传入任何想发送到服务器的字符串。



与 GET 请求相比，POST 请求消耗的资源会更多一些。从性能角度来看，以发送相同的数据计算，GET 请求的速度最多可达到 POST 请求的两倍。



### 例子

原生 Ajax 实现步骤

- 创建 XMLHttpRequest 对象，也就是创建一个异步调用对象。
- 设置响应 HTTP 请求状态变化的函数。（事件处理函数 onreadystatechange  ）
- 打开一个新的 HTTP 请求，并指定该 HTTP 请求的方法、URL 及验证信息。
- 通过 open 与服务器建立连接  
- 发送 HTTP 请求。
- 在响应回调函数中，根据改变状态和请求状态码，获取异步请求返回的数据。
- 渲染返回的数据。使用 JavaScript 和 DOM 实现局部刷新。



```js
document.getElementById("search").onclick = function() { 
    // 创建 XHR 对象
	var request = new XMLHttpRequest();
    // 初始化请求
	request.open("GET", "server.php?number=" + document.getElementById("keyword").value);
    // 发送请求
	request.send();
    // readystatechange 事件
	request.onreadystatechange = function() {
        // 是否接收到全部响应数据
		if (request.readyState === 4) {
			if (request.status === 200) { 
                // 获得响应文本
				document.getElementById("searchResult").innerHTML = request.responseText;
			} else {
				alert("发生错误：" + request.status);
			}
		} 
	}
}
```









## 2. XMLHttpRequest 2 级

并非所有浏览器都完整地实现了 XMLHttpRequest 2 级规范，但所有浏览器都实现了它规定的部分内容。



### FormDate

FormData 为序列化表单以及创建与表单格式相同的数据（用于通过XHR 传输）提供
了便利。下面的代码创建了一个 FormData 对象，并向其中添加了一些数据。

```js
var data = new FormData();
data.append("name", "Nicholas");
```

创建了FormData 的实例后，可以将它直接传给 XHR 的 send() 方法



使用 FormData 的方便之处体现在不必明确地在 XHR 对象上设置请求头部。XHR 对象能够识别传入的数据类型是 FormData 的实例，并配置适当的头部信息。

支持 FormData 的浏览器有 Firefox 4+、Safari 5+、Chrome 和 Android 3+ 版 WebKit。



### 超时设定



### overrideMimeType()









## 3. 进度事件

Progress Events 规范是 W3C 的一个工作草案，定义了与客户端服务器通信有关的事件。这些事件最早其实只针对 XHR 操作，但目前也被其他 API 借鉴。有以下6 个进度事件。

-  loadstart：在接收到响应数据的第一个字节时触发。
-  progress：在接收响应期间持续不断地触发。
-  error：在请求发生错误时触发。
-  abort：在因为调用abort()方法而终止连接时触发。
-  load：在接收到完整的响应数据时触发。
-  loadend：在通信完成或者触发error、abort 或load 事件后触发。

每个请求都从触发 loadstart 事件开始，接下来是一或多个 progress 事件，然后触发 error、abort 或 load 事件中的一个，最后以触发 loadend 事件结束。

支持前5 个事件的浏览器有Firefox 3.5+、Safari 4+、Chrome、iOS 版Safari 和Android 版WebKit。Opera（从第11 版开始）、IE 8+只支持load 事件。目前还没有浏览器支持loadend 事件。



### load 事件



### progress 事件









# 参考链接

- [Ajax 全接触 - 慕课网课程](https://www.imooc.com/learn/250)
- [AJAX 教程 - 菜鸟教程](https://www.runoob.com/ajax/ajax-tutorial.html)
- [XMLHttpRequest - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)
- [XMLHttpRequest.readyState - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/readyState)
- 锋利的 jQuery [M].





