# 六、性能 & 集成

## Web Worker 

**什么是 Web Worker？**

当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。

web worker 是**运行在后台的 JavaScript**，独立于其他脚本，**不会影响页面的性能**。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 Web worker 在后台运行。

浏览器支持：IE 10，Firefox，Chrome，Safari 和 Opera 都支持Web workers。



**例子：使用 Web Worker 创建计数器**

**检测浏览器是否支持 Web Worker**

在创建 web worker 之前，检测浏览器是否支持它：

```js
if(typeof(Worker)!=="undefined"){
  // 是的! Web worker 支持!
  // *一些代码.....*
}
else{
  //抱歉! Web Worker 不支持
}
```

**创建 web worker 文件**

在一个外部 JavaScript 中创建 web worker。

在下面的例子中，创建计数脚本并存储于 "demo_workers.js" 文件。 代码中重要的部分是postMessage() 方法 - 用于向 HTML 页面传回一段消息。

```js
var i=0;

function timedCount(){
  i=i+1;
  postMessage(i);		// 代码中重要的部分
  setTimeout("timedCount()",500);
}

timedCount();
```

**创建 Web Worker 对象**

需要从 HTML 页面调用 web worker 文件。

下面的代码检测是否存在 worker，如果不存在，它会创建一个新的 web worker 对象，然后运行 "demo_workers.js" 中的代码：

```js
if(typeof(w)=="undefined"){
  w = new Worker("demo_workers.js");
}
```

然后我们就可以从 web worker 发生和接收消息了。

向 web worker 添加一个 "onmessage" 事件监听器：

```js
w.onmessage=function(event){
  document.getElementById("result").innerHTML=event.data;
};
```

**终止 Web Worker**

创建 web worker 对象后，它会继续监听消息（即使在外部脚本完成之后）直到其被终止为止。

如需终止 web worker，并释放浏览器/计算机资源，使用 terminate() 方法：

```js
w.terminate();
```

**完整的代码**

```html
<p>计数： <output id="result"></output></p>
<button onclick="startWorker()">开始工作</button> 
<button onclick="stopWorker()">停止工作</button>
<p><strong>注意：</strong> I9 及更早 IE 版本浏览器不支持 Web Workers.</p>

<script>
var w;
 
function startWorker() {
    if(typeof(Worker) !== "undefined") {
        if(typeof(w) == "undefined") {
            w = new Worker("demo_workers.js");
        }
        w.onmessage = function(event) {
            document.getElementById("result").innerHTML = event.data;
        };
    } else {
        document.getElementById("result").innerHTML = "抱歉，你的浏览器不支持 Web Workers...";
    }
}
 
function stopWorker() 
{ 
    w.terminate();
    w = undefined;
}
</script>
```



**Web Workers 和 DOM**

由于 web worker 位于外部文件中，它们无法访问下列 JavaScript 对象：

- window 对象
- document 对象
- parent 对象



## History API





## 拖放

拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放（drag 和 drop）是标准的一部分，任何元素都能够拖放。

浏览器支持：IE 9+，Firefox，Opera，Chrome 和 Safari 支持拖动。

**注意：**Safari 5.1.2不支持拖动。



**一个简单的拖放实例**

**设置元素为可拖放**

首先，为了使元素可拖动，把 draggable 属性设置为 true ：

```html
<img draggable="true">
```

**拖动什么 - ondragstart 和 setData()**

然后，规定当元素被拖动时，会发生什么。

在下面的例子中，ondragstart 属性调用了一个函数 drag(event)，它规定了被拖动的数据。dataTransfer.setData() 方法设置被拖数据的数据类型和值：

```js
function drag(ev){
  ev.dataTransfer.setData("Text",ev.target.id);
}
```

Text 是一个 DOMString 表示要添加到 drag object 的拖动数据的类型。值是可拖动元素的 id ("drag1")。

**放到何处 - ondragover**

ondragover 事件规定在何处放置被拖动的数据。

默认地，无法将数据/元素放置到其他元素中。如果需要设置允许放置，我们必须阻止对元素的默认处理方式。

这要通过调用 ondragover 事件的 event.preventDefault() 方法：

```js
event.preventDefault()
```

**进行放置 - ondrop**

当放置被拖数据时，会发生 drop 事件。

在下面的例子中，ondrop 属性调用了一个函数，drop(event)：

```js
function drop(ev){
  ev.preventDefault();
  var data=ev.dataTransfer.getData("Text");
  ev.target.appendChild(document.getElementById(data));
}
```

代码解释：

- 调用 preventDefault() 来避免浏览器对数据的默认处理（drop 事件的默认行为是以链接形式打开）
- 通过 dataTransfer.getData("Text") 方法获得被拖的数据。该方法将返回在 setData() 方法中设置为相同类型的任何数据。
- 被拖数据是被拖元素的 id ("drag1")
- 把被拖元素追加到放置元素（目标元素）中

**完整的代码**

```html
<!-- 矩形框的样式 -->
<style type="text/css">
#div1 {width:350px;height:70px;padding:10px;border:1px solid #aaaaaa;}
</style>

<script>
// 第三步：放到何处
function allowDrop(ev){
    ev.preventDefault();
}
// 第二步：拖动什么 
function drag(ev){
    ev.dataTransfer.setData("Text",ev.target.id);
}
// 第四步：进行放置
function drop(ev){
    ev.preventDefault();
    var data=ev.dataTransfer.getData("Text");
    ev.target.appendChild(document.getElementById(data));
}
</script>

<p>拖动下面的图片到矩形框中:</p>
<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)"></div>
<br>
<!-- 第一步：设置元素为可拖放 -->
<img id="drag1" src="/images/logo.png" draggable="true" ondragstart="drag(event)" width="336" height="69">
```

更多实例：[来回拖放图片-菜鸟教程](https://www.runoob.com/try/try.php?filename=tryhtml5_draganddrop2)



## 焦点管理



## 全屏API











# 七、设备访问



## 地理定位

### geolocation 对象

地理位置 API 通过 [`navigator.geolocation`](https://developer.mozilla.org/zh-CN/docs/Web/API/NavigatorGeolocation/geolocation) 提供。

```js
if ("geolocation" in navigator) {
  /* 地理位置服务可用 */
} else {
  /* 地理位置服务不可用 */
}
```

**获取当前定位**

调用 `getCurrentPosition()` 函数获取用户当前定位位置。

这会异步地请求获取用户位置，并查询定位硬件来获取最新信息。当定位被确定后，定义的回调函数就会被执行。您可以选择性地提供第二个回调函数，当有错误时会被执行。第三个参数也是可选的，您可以通过该对象参数设定最长可接受的定位返回时间、等待请求的时间和是否获取高精度定位。

**监视定位**

通过 `watchPosition()` 函数实现该功能。它与 `getCurrentPosition()` 接受相同的参数，但回调函数会被调用多次。错误回调函数与 `getCurrentPosition()` 中一样是可选的，也会被多次调用。

**调整返回结果**

`getCurrentPosition()` 和 `watchPosition()` 都接受一个成功回调、一个可选的失败回调和一个可选的 `PositionOptions` 对象。

























