

# 三、其它嵌入技术

`<iframe>` 允许将其他 Web 文档嵌入到当前文档中，`<embed>` 和 `<object>` 允许嵌入PDF，SVG，甚至 Flash。`<iframe>` 现在经常被使用。

```html
<iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p> <a href="https://developer.mozilla.org/en-US/docs/Glossary">
    Fallback link for browsers that don't support iframes
  </a> </p>
</iframe>
```

此示例包括使用以下所需的 `<iframe>` 基本要素：

- `allowfullscreen`

  通过[全屏API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fullscreen_API)设置为全屏模式（稍微超出本文的范围）。

- `frameborder`

  如果设置为1，则会告诉浏览器在此框架和其他框架之间绘制边框，这是默认行为。0，删除边框。不推荐这样设置，因为在 CSS 中可以更好地实现相同的效果。`border: none;`

- `src`

  该属性与 `<video>` /`<img>` 一样包含指向要嵌入文档的 URL 路径。

- `width` 和 `height`

  这些属性指定您想要的 iframe 的宽度和高度。

- 备选内容

  与 `<video>` 等其他类似元素相同，您可以在 `<iframe>` `</iframe>` 标签之间包含备选内容，如果浏览器不支持 `<iframe>`，将会显示备选内容，这种情况下，我们已经添加了一个到该页面的链接。现在几乎不可能遇到任何不支持 `<iframe>` 的浏览器。

- `sandbox`

  该属性需要在已经支持其他 `<iframe>` 功能（例如 IE 10 及更高版本）但稍微更现代的浏览器上才能工作，该属性可以提高安全性设置。

> **注意**：为了提高速度，在主内容完成加载后，使用 JavaScript 设置 iframe 的 `src `属性是个好主意。这使您的页面可以更快地被使用，并减少您的官方页面加载时间（重要的[SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO)指标）。



### 安全隐患



如果**黑客**试图恶意修改网页或欺骗人们进行不想做的事情时常把 iframe 作为共同的攻击目标（官方术语：**攻击向量**），例如显示用户名和密码等敏感信息。因此，规范工程师和浏览器开发人员已经开发了各种安全机制，使 `<iframe>` 更加安全。

> [单击劫持](https://en.wikipedia.org/wiki/Clickjacking)是一种常见的 iframe 攻击，黑客将隐藏的 iframe 嵌入到您的文档中（或将您的文档嵌入到他们自己的恶意网站），并使用它来捕获用户的交互。这是误导用户或窃取敏感数据的常见方式。





#### 只有在必要时嵌入

有时嵌入第三方内容（例如 YouTube 视频和地图）是有意义的，但如果您只在完全需要时嵌入第三方内容，您可以省去很多麻烦。

网络安全的一个很好的经验法则是*“你怎么谨慎都不为过，如果你决定要做这件事，多检查一遍；如果是别人做的，在被证明是安全的之前，都假设这是危险的。”*

除了安全问题，你还应该意识到知识产权问题。无论在线内容还是离线内容，绝大部分内容都是有版权的，甚至是一些你没想到有版权的内容。不要在网页上展示一些不属于你的内容，除非你是所有者或所有者给了你明确的、书面的许可。

如果内容获得许可，你必须遵守许可条款。例如，MDN上的内容是[在CC-BY-SA下许可的](https://developer.mozilla.org/zh-CN/docs/MDN/About#版权和许可)，这意味着，如果你要引用我们的内容，就必须[用适当的方式注明来源](https://wiki.creativecommons.org/wiki/Best_practices_for_attribution)，即使你对内容做了实质性的修改。

#### 使用 HTTPS

[HTTPS](https://developer.mozilla.org/en-US/docs/Glossary/HTTPS)是[HTTP](https://developer.mozilla.org/en-US/docs/Glossary/HTTP)的加密版本。您应该尽可能使用 HTTPS 为您的网站提供服务：

1. HTTPS 减少了远程内容在传输过程中被篡改的机会，
2. HTTPS 防止嵌入式内容访问您的父文档中的内容，反之亦然。

使用 HTTPS 需要一个安全证书，这可能是昂贵的（尽管[Let's Encrypt](https://letsencrypt.org/)让这件事变得更容易），如果你没有，可以使用 HTTP 来为你的父文档提供服务。但是，由于HTTPS的第二个好处，*无论成本如何，您绝对不能使用HTTP嵌入第三方内容*（在最好的情况下，您的用户的Web浏览器会给他们一个可怕的警告）。所有有声望的公司，例如 Google Maps 或 Youtube，当您嵌入内容时，`<iframe>` 将通过HTTPS提供 - 查看`<iframe>`  `src` 属性内的URL。

> **注意**：[Github页面](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Using_Github_pages)允许默认情况下通过HTTPS提供内容，因此对托管内容很有用。如果您正在使用不同的托管，并且不确定，请向您的托管服务商询问。

#### 始终使用 `sandbox` 属性

想尽可能减少攻击者在你的网站上做坏事的机会，那么你应该给嵌入的内容仅能完成自己工作的权限*。*当然，这也适用于你自己的内容。一个允许包含在其里的代码以适当的方式执行或者用于测试，但不能对其他代码库（意外或恶意）造成任何损害的容器称为[沙盒](https://en.wikipedia.org/wiki/Sandbox_(computer_security))。

未沙盒化(Unsandboxed)内容可以做得太多（执行JavaScript，提交表单，弹出窗口等）默认情况下，您应该使用没有参数的`sandbox`属性来强制执行所有可用的限制，如我们前面的示例所示。

如果绝对需要，您可以逐个添加权限（`sandbox=""`属性值内） - 请参阅`sandbox `所有可用选项的参考条目。其中重要的一点是，你*永远不*应该同时添加 `allow-scripts` 和 `allow-same-origin` 到你的 `sandbox` 属性中-在这种情况下，嵌入式内容可以绕过阻止站点执行脚本的同源安全策略，并使用 JavaScript 完全关闭沙盒。

> **注意**：如果攻击者可以欺骗人们直接访问恶意内容（在iframe之外），则沙盒无法提供保护。如果某些内容可能是恶意的（例如，用户生成的内容），请保证其是从不同的[域](https://developer.mozilla.org/en-US/docs/Glossary/domain)向您的主站点提供的。

#### 配置CSP指令

[CSP](https://developer.mozilla.org/en-US/docs/Glossary/CSP) 代表**[内容安全策略](https://developer.mozilla.org/en-US/docs/Web/Security/CSP)**，它提供[一组HTTP标头](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/CSP_policy_directives)（由web服务器发送时与元数据一起发送的元数据），旨在提高HTML文档的安全性。在``s安全性方面，您可以*[将服务器配置为发送适当的`X-Frame-Options` 标题。](https://developer.mozilla.org/en-US/docs/Web/HTTP/X-Frame-Options)*这样做可以防止其他网站在其网页中嵌入您的内容（这将导致[点击](https://en.wikipedia.org/wiki/clickjacking)和一系列其他攻击），正如我们之前看到的那样，MDN开发人员已经做了这些工作。

> **注意**：您可以阅读Frederik Braun的帖子[在X-Frame-Options安全性头上](https://blog.mozilla.org/security/2013/12/12/on-the-x-frame-options-security-header/)来获取有关此主题的更多背景信息。显然，在这篇文章中已经解释得很清楚了。

## `<embed>` 和 `<object>` 元素

`<embed>` 和 `<object>` 元素的功能不同于`<iframe>` —— 这些元素是用来嵌入多种类型的外部内容的通用嵌入工具，其中包括像 Java 小程序和Flash，PDF（可在浏览器中显示为一个PDF插件）这样的插件技术，甚至像视频，SVG和图像的内容！

> **注意**：**插件**是一种对浏览器原生无法读取的内容提供访问权限的软件。

然而，您不太可能使用这些元素 - Applet 几年来一直没有被使用；由于许多原因，Flash 不再受欢迎（见下面的[插件案例](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Other_embedding_technologies#The_case_against_plugins)）；PDF更倾向于被链接而不是被嵌入；其他内容，如图像和视频都有更优秀、更容易元素来处理。插件和这些嵌入方法真的是一种传统技术，我们提及它们主要是为了以防您在某些情况下遇到问题，比如内部网或企业项目等。

如果您发现自己需要嵌入插件内容，那么您至少需要一些这样的信息：

|                                                              | `<embed>`                    | `<object>`                              |
| :----------------------------------------------------------- | :--------------------------- | :-------------------------------------- |
| 嵌入内容的[网址](https://developer.mozilla.org/en-US/docs/Glossary/URL) | `src`                        | `data`                                  |
| 嵌入内容的*准确*[媒体类型](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type) | `type`                       | `type`                                  |
| 由插件控制的框的高度和宽度（以CSS像素为单位）                | `height` `width`             | `height` `width`                        |
| 名称和值，将插件作为参数提供                                 | 具有这些名称和值的ad hoc属性 | 单标签`<param>`元素，包含在内`<object>` |
| 独立的HTML内容作为不可用资源的回退                           | 不支持（`<noembed>`已过时）  | 包含在元素`<object>` 之后`<param>`      |

> **注意**：`<object>` 需要 `data `属性，`type `属性或两者。如果您同时使用这两个，您也可以使用该 `typemustmatch` 属性（仅在 Firefox 中实现，在本文中）。`typemustmatch `保持嵌入文件不运行，除非 `type` 属性提供正确的媒体类型。`typemustmatch` 因此，当您嵌入来自不同[来源的](https://developer.mozilla.org/en-US/docs/Glossary/origin)内容（可以防止攻击者通过插件运行任意脚本）时，可以赋予重要的安全优势。

下面是一个使用该 `<embed>`元素嵌入 Flash 影片的示例：

```html
<embed src="whoosh.swf" quality="medium"
       bgcolor="#ffffff" width="550" height="400"
       name="whoosh" align="middle" allowScriptAccess="sameDomain"
       allowFullScreen="false" type="application/x-shockwave-flash"
       pluginspage="http://www.macromedia.com/go/getflashplayer">
```

很可怕，不是吗 。Adobe Flash工具生成的HTML往往更糟糕，使用嵌入`<object>` 元素的 `<embed>` 元素来覆盖所有的基础（查看一个例子）。甚至有一段时间，Flash被成功地用作HTML5视频的备用内容，但是这种情况越来越被认为是不必要的。

现在来看一个 `<object>` 将PDF嵌入一个页面的例子：

```html
<object data="mypdf.pdf" type="application/pdf"
        width="800" height="1200" typemustmatch>
  <p>You don't have a PDF plugin, but you can <a href="myfile.pdf">download the PDF file.</a></p>
</object>
```

PDF是纸与数据之间重要的阶梯，但它们[在可访问性上有些问题](http://webaim.org/techniques/acrobat/acrobat)[，](http://webaim.org/techniques/acrobat/acrobat)并且可能难以在小屏幕上阅读。它们在一些圈子中仍然受欢迎，我们最好是用链接指向它们，而不是将其嵌入到网页中，以便它们可以在单独的页面上被下载或被阅读。

### 针对插件的情况



以前，插件在网络上是不可或缺的。还记得你必须安装Adobe Flash Player才能在线观看电影的日子吗？并且你还会不断地收到关于更新Flash Player和Java运行环境的烦人警报。Web技术已经变得更加强大，那些日子已经结束了。对于大多数应用程序，现在是停止依赖插件传播内容，开始利用Web技术的时候了。

- **扩大你对大家的影响力。**每个人都有一个浏览器，但插件越来越少，特别是在移动用户中。由于Web在很大程度上不需要依赖插件而运行，所以人们宁愿只是去竞争对手的网站而不是安装插件。
- **从Flash和其他插件附带的[额外的可访问性问题](http://webaim.org/techniques/flash/)中摆脱。**
- **避免额外的安全隐患。**即使经过无数次补丁[，](http://www.cvedetails.com/product/6761/Adobe-Flash-Player.html?vendor_id=53) Adobe Flash也是[非常不安全的](http://www.cvedetails.com/product/6761/Adobe-Flash-Player.html?vendor_id=53)。2015年，Facebook的首席安全官Alex Stamos甚至[要求Adobe停止Flash。](http://www.theverge.com/2015/7/13/8948459/adobe-flash-insecure-says-facebook-cso)

那你该怎么办？如果您需要交互性，HTML和[JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript)可以轻松地为您完成工作，而不需要Java小程序或过时的ActiveX / BHO技术。您可以使用[HTML5视频](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)来满足媒体需求，矢量图形[SVG](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Adding_vector_graphics_to_the_Web)，以及复杂图像和动画[画布](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)。[彼得·埃尔斯特（Peter Elst）几年前已经提到](https://plus.google.com/+PeterElst/posts/P5t4pFhptvp)，对于工作Adobe Flash极少是正确的工具，除了专门的游戏和商业应用。对于ActiveX，即使微软的[Edge](https://developer.mozilla.org/en-US/docs/Glossary/Microsoft_Edge)浏览器也不再支持。



