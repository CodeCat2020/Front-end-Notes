



# 二、音频和视频

注意：`<video>` 、 `<audio>` 、`<embed>` 是 HTML5 标签，在 HTML4 中是非法的，页面无法通过 HTML4 验证。但是在所有浏览器中都有效。使用 `<!DOCTYPE html>` (HTML5) 解决验证问题。



##  HTML5 `<video>` 

 `<video>` 是 HTML 5 中的新标签，作用是在 HTML 页面中嵌入**视频**元素。

```html
<video src="rabbit320.webm" controls>
  <p>你的浏览器不支持 HTML5 视频。可点击<a href="rabbit320.mp4">此链接</a>观看</p>
</video>
```



 `<video>` 的属性如下：

- `src` ：指向嵌入网页当中的视频资源。同 `<img>` 标签使用方式相同。

- `controls`

  用户必须能够控制视频和音频的**回放功能**，包括开始、停止以及调整音量的功能。可以使用浏览器提供的控制接口，也可以使用合适的 [JavaScript API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement) 构建控制接口。

- `<video>` 标签内的段落

  **后备内容** 。当浏览器不支持 `<video>` 标签时，会显示出来，能够对旧的浏览器做一些兼容处理。

已嵌入视频文件的网页样式如下：

![A simple video player showing a video of a small white rabbit](https://mdn.mozillademos.org/files/12794/simple-video.png)

问题

- 您必须把视频转换为很多不同的格式。
- `<video>` 元素在老式浏览器中无效。
- `<video>` 元素无法通过 HTML4 和 XHTML 验证。



### 多格式支持 `<source>`

 `<source>` 定义多个数据源

像 MP3、MP4、WebM 这些术语叫做**容器格式**。他们定义了组成媒体文件的音频轨道和视频轨道存储的方式，描述这个媒体文件的元数据，以及用于编码的编码译码器。

格式为 WebM 的电影包含视频轨道，音频轨道和文本轨道，其中视频轨道包含一个主视频轨道和一个可选的 Angle 轨道；音频轨道包含英语和西班牙语的音频轨道，还有一个英语评论的音频轨道；文字轨道包含英语和西班牙语的字幕轨道，如下图所示：

![Diagram conceptualizing the contents of a media file at the track level.](https://mdn.mozillademos.org/files/16898/ContainersAndTracks.svg)

上图所示这个容器中的音频轨道和视频轨道中的数据可以被解码编码器用于对这个媒体文件编码，视频和音频都有不同的格式，如下:

- WebM 容器通常包括了 Opus 或 Vorbis 音频和 VP8/VP9 视频。这在所有的现代浏览器中都支持，除了他们的老版本。
- MP4 容器通常包括 AAC 以及 MP3 音频和 H.264 视频。这在所有的现代浏览器中都支持，还有 Internet Explorer。
- 老式的 Ogg 容器往往支持 Ogg Vorbis  音频和 Ogg Theora 视频。主要在 Firefox 和 Chrome 当中支持，不过这个容器已经被更强大的 WebM 容器所取代。

音频播放器将会直接播放音频文件，例如 MP3 和 Ogg 文件。这些不需要容器。

以上的格式主要用于将音频和视频压缩成可管理的文件（原始的音频和视频文件非常大）。浏览器包含了不同的 **[Codecs](https://developer.mozilla.org/zh-CN/docs/Glossary/Codec)**,，如 Vorbis 和 H.264,，它们用来将已压缩的音频和视频转化成二进制数字。正如刚才所说，浏览器并不全支持相同的 codecs，所以你得使用几个不同格式的文件来兼容不同的浏览器。如果你使用的格式都得不到浏览器的支持，那么媒体文件将不会播放。



我们该怎么做呢？请看如下例子：

```html
<video controls>
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>你的浏览器不支持 HTML5 视频。可点击<a href="rabbit320.mp4">此链接</a>观看</p>
</video>
```

现在我们将 `src` 属性从  `<video>`  标签中移除，转而将它放在几个单独的标签  `<source>`  当中。在这个例子当中，浏览器将会检查  `<source>`   标签，并且播放第一个与其自身 codec 相匹配的媒体。你的视频应当包括 WebM 和 MP4 两种格式，这两种在目前已经足够支持大多数平台和浏览器。

每个 `<source>`  标签页含有一个 `type` 属性，这个属性是可选的，但是建议你添加上这个属性 — 它包含了视频文件的 [MIME types](https://developer.mozilla.org/zh-CN/docs/Glossary/MIME_type) ，同时浏览器也会通过检查这个属性来迅速的跳过那些不支持的格式。如果你没有添加 `type` 属性，浏览器会尝试加载每一个文件，直到找到一个能正确播放的格式，这样会消耗掉大量的时间和资源。



### 其他 `<video>` 特性

```html
<video controls width="400" height="400"
       autoplay loop muted
       poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>你的浏览器不支持 HTML5 视频。可点击<a href="rabbit320.mp4">此链接</a>观看</p>
</video>
```

 HTML5  `<video>` 上的特性：

- `width` 和 `height`

  可以用属性控制视频的尺寸，也可以用 CSS 来控制视频尺寸。无论使用哪种方式，视频都会保持它原始的长宽比（或**纵横比**） 。如果你设置的尺寸没有保持视频原始长宽比，那么视频边框将会拉伸，而未被视频内容填充的部分，将会显示默认的背景颜色。

- `autoplay`

  使音频和视频内容立即播放，即使页面的其他部分还没有加载完全。建议不要使用。

- `loop`

  让音频或者视频文件循环播放。除非有必要，不建议使用。

- `muted`

  媒体播放时，默认关闭声音。

- `poster`

  指向了一个图像的 URL，这个图像会在视频播放前显示。通常用于粗略的预览或者广告。

- `preload`

  用来缓冲较大的文件，有3个值可选：`"none"` ：不缓冲 `"auto"` ：页面加载后缓存媒体文件`"metadata"` ：仅缓冲文件的元数据







##  HTML5 `<audio>` 

 `<audio>` 是 HTML 5 中的新标签，作用是在 HTML 页面中嵌入**音频**元素。

```html
<audio controls="controls">
  <!--mp3 文件在 IE、Chrome 以及 Safari 中是有效的-->
  <source src="song.mp3" type="audio/mp3" />
  <!--ogg 文件在 Firefox 和 Opera 中是有效的-->
  <source src="song.ogg" type="audio/ogg" />
Your browser does not support this audio format.
</audio>
```

 `<audio>` 与  `</audio>` 之间插入的内容是供不支持 `<audio>` 元素的浏览器显示的。

问题：

-  必须把音频文件转换为不同的格式。
-  `<audio>` 元素在老式浏览器中不起作用。



 `<audio>` 标签与  `<video>` 标签的使用方式几乎完全相同，有一些细微的差别不同：

-  因为其没有视觉部件，音频播放器所占用的空间比视频播放器要小。
-  因为其没有视觉部件，`<audio>` 标签不支持 `width`/`height` 属性， `poster` 属性。
-  除此之外，`<audio>`  标签支持所有 `<video>` 标签拥有的特性。





## 使用插件

浏览器插件是一种扩展浏览器标准功能的小型计算机程序。插件有很多用途：播放音乐、显示地图、验证银行账号，控制输入等等。

可使用 `<object>` 或 `<embed>` 标签来将插件添加到 HTML 页面。这些标签定义资源（通常非 HTML 资源）的容器，根据类型，它们即会由浏览器显示，也会由外部插件显示。

问题：

- 不同的浏览器对音频格式的支持不同。

- 浏览器可能不支持该文件格式。

- 可能未安装插件。

- 把该文件转换为其他格式，仍然无法在所有浏览器中播放。



### HTML5 `<embed>` 

`<embed>` 标签是定义外部（非 HTML）内容的容器，作用是在 HTML 页面中**嵌入多媒体元素**。

```html
<!--显示嵌入网页中的 MP3 文件-->
<embed height="100" width="100" src="song.mp3" />
<!--显示嵌入网页的 Flash 视频-->
<embed height="200" width="200" src="movie.swf" />
```

其它问题：

- 如果浏览器不支持 Flash，那么视频将无法播放
- iPad 和 iPhone 不能显示 Flash 视频。



###  `<object>` 元素

`<object>` 标签也可以定义外部（非 HTML）内容的容器，作用是在 HTML 页面中嵌入多媒体元素。

显示嵌入网页中的 MP3 文件：

```html
<object height="100" width="100" data="song.mp3"></object>
```

显示嵌入网页的一段 Flash 视频：

```html
<object height="200" width="200" data="movie.swf" />
```

问题与使用 `<embed>` 嵌入 Flash 视频一样。



## HTML5 `<track>`

存在一些情况不想（或者不能）听到 Web 上的音频/视频内容，比如：有听觉障碍、非常嘈杂的环境或非常安静的环境、听不懂（需要副本或翻译）。“副本”指，用文本记录下音频的内容。

`<track>` 标签是 HTML 5 中的新标签，为 `<video>` 和 `<audio> ` 等媒介规定外部文本轨道，用于规定字幕文件或其他包含文本的文件。

当媒介播放时，这些文件是**可见的**。目前所有主流浏览器都不支持 `<track>` 标签。

```html
<video controls>
    <source src="example.mp4" type="video/mp4">
    <source src="example.webm" type="video/webm">
    <track kind="subtitles" src="subtitles_en.vtt" srclang="en">
</video>
```

 `<track>` 标签需放在 `<audio>` 或   `<video>` 标签中，同时需要放在所有 `<source>` 标签之后。使用 `kind` 属性来指明是哪一种类型，如 subtitles 、 captions 、 descriptions。然后，使用 `srclang` 来告诉浏览器你是用什么语言来编写的 subtitles。

> 文本轨道会使你的网站更容易被搜索引擎抓取到 （[SEO](https://developer.mozilla.org/zh-CN/docs/Glossary/SEO)）， 由于搜索引擎的文本抓取能力非常强大，使用文本轨道甚至可以让搜索引擎通过视频的内容直接链接。









## 最好的 HTML 解决方法

### 音频

  `<audio>` +  `<embed>`

```html
<audio controls="controls" height="100" width="100">
  <source src="song.mp3" type="audio/mp3" />
  <source src="song.ogg" type="audio/ogg" />
  <embed height="100" width="100" src="song.mp3" />
</audio>
```

上面的例子使用了两个不同的音频格式。 `<audio>` 元素会尝试以 mp3 或 ogg 来播放音频。如果失败，代码将回退尝试 `<embed>` 元素。

问题：

- 必须把音频转换为不同的格式。
- `<embed>` 元素无法回退来显示错误消息。



### 视频

  `<video>`  + `<object>` + `<embed>`

```html
<video width="320" height="240" controls="controls">
  <source src="movie.mp4" type="video/mp4" />
  <source src="movie.ogg" type="video/ogg" />
  <source src="movie.webm" type="video/webm" />
  <object data="movie.mp4" width="320" height="240">
    <embed src="movie.swf" width="320" height="240" />
  </object>
</video>
```

上例中使用了 4 中不同的视频格式。 `<video>` 元素会尝试播放以 mp4、ogg 或 webm 格式中的一种来播放视频。如果均失败，则回退到 `<embed>` 元素。

问题

- 必须把视频转换为很多不同的格式



## 最简单方法

### 雅虎的媒体播放器

使用雅虎媒体播放器是一个不同的途径。只需简单地让雅虎来完成歌曲播放的工作。

它能播放 mp3 以及一系列其他格式。通过一行简单的代码，您就可以把它添加到网页中，轻松地将 HTML 页面转变为专业的播放列表。

使用雅虎播放器是免费的。如需使用它，您需要把这段 JavaScript 插入网页底部：

```html
<script type="text/javascript" src="http://mediaplayer.yahoo.com/js"></script>
```

然后只需简单地把 MP3 文件链接到您的 HTML 中，JavaScript 会自动地为每首歌创建播放按钮：

```html
<a href="song1.mp3">Play Song 1</a>
<a href="song2.mp3">Play Song 2</a>
...
```

雅虎媒体播放器为用户提供一个小型的播放按钮，而不是完整的播放器。不过，当您点击该按钮，会弹出完整的播放器。

请注意，这个播放器始终停靠在窗框底部。只需点击它，就可将其滑出。



### 优酷解决方案

在 HTML 中显示视频的最简单的方法是使用优酷等视频网站。

把视频上传到优酷等视频网站，然后网页中插入 HTML 代码即可在网页中播放视频：

```html
<embed src="http://player.youku.com/player.php/sid/XMzI2NTc4NTMy/v.swf" 
width="480" height="400" 
type="application/x-shockwave-flash">
</embed>
```



## 使用超链接

如果网页包含指向媒体文件的超链接，大多数浏览器会使用“辅助应用程序”来播放文件。

以下代码片段显示指向 mp3 文件的链接。如果用户点击该链接，浏览器会启动“辅助应用程序”来播放该文件：

```html
<a href="song.mp3">Play the sound</a>
```

以下代码片段显示指向 AVI 文件的链接。如果用户点击该链接，浏览器会启动“辅助应用程序”，比如 Windows Media Player 来播放这个 AVI 文件：

```html
<a href="movie.swf">Play a video file</a>
```





## 内联声音/视频

内联声音/视频：在网页中包含声音/视频，或者作为网页的组成部分。

很多人都觉得内联声音令人恼火。

同时请注意，用户可能已经关闭了浏览器中的内联声音/视频选项。

我们最好的建议：只在用户希望听到内联声音/视频的地方包含它们。一个正面的例子是，在用户需要听到录音/看到视频并点击某个链接时，会打开页面然后播放录音/视频。





## 小结

HTML 4.01 多媒体标签

| 标签       | 描述                                         |
| :--------- | :------------------------------------------- |
| `<applet>` | 不赞成。定义内嵌 applet。                    |
| `<embed>`  | HTML4 中不赞成，HTML5 中允许。定义内嵌对象。 |
| `<object>` | 定义内嵌对象。                               |
| `<param>`  | 定义对象的参数。                             |

HTML 5 多媒体标签

| 标签      | 描述                                 |
| :-------- | :----------------------------------- |
| `<audio>` | 标签定义声音，比如音乐或其他音频流。 |
| `<video>` | 标签定义声音，比如音乐或其他音频流。 |
| `<embed>` | 标签定义嵌入的内容，比如插件。       |


