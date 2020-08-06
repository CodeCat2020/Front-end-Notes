# 一、HTML 图片

用 `<img>` 元素来把图片放到网页上。它是一个空元素，不需要包含文本内容或闭合标签，最少只需要一个 **`src`** （ *source）*来使其生效。

##  `<img>` 属性

### 图片路径 `src`

`src` 属性包含了图片的路径，可以是相对路径或绝对 URL，就像 `a` 元素的 `href` 属性一样。

图片 `dinosaur.jpg` ，与当前 HTML 页面存放在相同路径下：

```html
<img src="dinosaur.jpg">
```

图片存储在和 HTML 页面同路径的 `images` 文件夹下（Google 推荐，利于 SEO/索引）：

```html
<img src="images/dinosaur.jpg">
```

> **注意：**搜索引擎也读取图像的文件名并把它们计入 SEO。因此你应该给你的图片取一个描述性的文件名：`dinosaur.jpg` 比 `img835.png `要好。

也可以使用绝对路径：

```html
<img src="https://www.example.com/images/dinosaur.jpg">
```

不推荐绝对路径方式，这样会使浏览器做更多的工作，例如重新通过 DNS 再去寻找 IP 地址。通常我们都会把图片和 HTML 放在同一个服务器上。

> **警告：**大多数图片是有版权的。**不要**在你的网页上使用一张图片，除非：
>
> 1. 你是图片版权所有者
> 2. 你有图片版权所有者明确的、书面上的使用授权
> 3. 你有充分的证据证明这张图片是公共领域内的
>
> 侵犯版权是违法并且不道德的。此外，在得到授权之前**永远不要**把你的`src`属性指向其他人网站上的图片。这被称为"盗链（hotlinking）"。同样，盗取其他人的带宽也是违法的。而且这会降低你的页面的加载速度，而且图片可能会在不受你控制的情况下被移走或用别的令人尴尬的东西替换掉。

**注意：**像 `<img>` 和 `<video>` 这样的元素有时被称之为**替换元素**，因为这样的元素的内容和尺寸由外部资源（像是一个图片或视频文件）所定义，而不是元素自身。









### 备选文本 `alt` 

 `alt` 属性是对图片的文字描述，用于在图片无法显示或不能被看到的情况。

```html
<img src="images/dinosaur.jpg"
     alt="The head and torso of a dinosaur skeleton;
          it has a large head with long sharp teeth">
```

测试 `alt` 属性最简单的方式就是故意拼错图片文件名。

为什么需要备选文本？它可以派上用场的原因有很多：

- 用户有视力障碍，通过[屏幕阅读器](https://zh.wikipedia.org/wiki/螢幕閱讀器)来浏览网页 。
- 图片的路径或文件名可能打错。
- 浏览器不支持该图片类型，比如 Lynx等纯文本的浏览器。
- 提供一些文字描述来给搜索引擎使用，搜索引擎可能会将图片的文字描述和查询条件进行匹配。
- 带宽有限且贵时，用户关闭图片显示（在手机上十分普遍）以减少数据的传输。

应该在 `alt` 里写什么？取决于图片的作用。

- **装饰：** `alt=""` 。
- **内容：**如果图片提供了重要信息，在 `alt` 文本中简要的提供相同的信息。如果在主要文本中已经对图片进行了充分的描述，写 `alt=""` 就好。
- **链接：**如果把图片嵌套在 `<a>` 标签里，变成链接，还必须[提供无障碍的链接文本](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#用清晰的链接措辞。)。在这种情况下，你可以写在同一个 `<a>` 元素里，或者写在图片的 `alt` 属性里。
- **文本：**不应该将文本放到图像里。如果真的必须这么做，那就把文本也放到 `alt `里。



### 宽度和高度

height 与 width 属性用于设置图像的高度与宽度。

```html
<img src="images/dinosaur.jpg"
     alt="一只恐龙头部和躯干的骨架，它有一个巨大的头，长着锋利的牙齿。"
     width="400"
     height="341">
```

如果图像指定了高度和宽度，页面加载时会保留指定的尺寸。如果图片没有显示（比如：没有加载完成等），浏览器会为图片留下一定的空间。否则，加载页面时可能会破坏 HTML 页面的整体布局。

![The Images in HTML title, with dinosaur alt text, displayed inside a large box that results from width and height settings](https://mdn.mozillademos.org/files/12706/alt-text-with-width-height.png)

这是一件好事情——这使得页面加载的更快速更流畅。

然而，你不应该使用 HTML 属性来改变图片的大小。如果你把尺寸设定的太大，最终图片看起来会模糊；如果太小，会在下载远远大于你需要的图片时浪费带宽。如果你没有保持正确的[宽高比](https://zh.wikipedia.org/wiki/長寬比_(影像))，图片可能看起来会扭曲。在把图片放到你的网站页面之前，你应该使用图形编辑器使图片的尺寸正确。

**注意：**如果你需要改变图片的尺寸，你应该使用 CSS 而不是 HTML。



### 图片标题 `title`

类似于[超链接](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#使用添加支持信息)，可以给图片增加 `title` 属性来提供需要更进一步的支持信息。

```html
<img src="images/dinosaur.jpg"
     alt="一只恐龙头部和躯干的骨架，它有一个巨大的头，长着锋利的牙齿。"
     width="400"
     height="341"
     title="A T-Rex on display in the Manchester University Museum">
```

鼠标悬停时会显示 titte 内容。

![The dinosaur image, with a tooltip title on top of it that reads A T-Rex on display at the Manchester University Museum ](https://mdn.mozillademos.org/files/12708/image-with-title.png)

图片标题并不必须要包含有意义的信息，通常来说，将这样的支持信息放到主要文本中而不是附着于图片会更好。不过，在有些环境中这样做更有用，比如当没有空间显示提示时，也就是在图片栏中。

然而，这并不是推荐的——title有很多易访问性问题，主要是基于这样一个事实，即屏幕阅读器的支持是不可预测的，大多数浏览器都不会显示它，除非您在鼠标悬停时（例如：title无法访问键盘用户）。





## 图片格式

嵌入在 HTML文档中的图像格式可以是什么？

答：支持四种格式： gif、bmp 、png 和 jpg。不支持 tif。

jpg 、gif  和  png 格式的图片体积很小，很常见。bmp 格式虽然很清晰色彩丰富，但是所占内存很大，所以很少见。



##  `<figure>` 

通过为图片搭配说明文字的方式来解说图片，方法之一：

```html
<div class="figure">
  <img src="/images/dinosaur_small.jpg"
     alt="一只恐龙头部和躯干的骨架，它有一个巨大的头，长着锋利的牙齿。"
     width="400"
     height="341">
  <p>曼彻斯特大学博物馆展出的一只霸王龙的化石</p>
</div>
```

这是可以的 ，`<p>` 中包含了你需要的内容，以及方便使用 CSS 的一种很好的风格。但是这里有一个问题 ，从语义的角度上来讲，`<img>` 和`<p>` 并没有什么联系，这会给使用屏幕阅读的人造成问题，比如当你有 50 张图片和其搭配的 50 段说明文字，那么一段说明文字是和哪张图片有关联的呢？

有一个更好的做法是使用 HTML5 的 `<figure>` 和 `<figcaption>` 元素，它正是为此而被创造出来的：为图片提供一个语义容器，在标题和图片之间建立清晰的关联。我们之前的例子可以重写为：

```html
<figure>
  <img src="https://raw.githubusercontent.com/mdn/learning-area/master/html/multimedia-and-embedding/images-in-html/dinosaur_small.jpg"
     alt="一只恐龙头部和躯干的骨架，它有一个巨大的头，长着锋利的牙齿。"
     width="400"
     height="341">
  <figcaption>曼彻斯特大学博物馆展出的一只霸王龙的化石</figcaption>
</figure>
```

  `<figcaption>` 告诉浏览器和其他辅助的技术工具这段说明文字描述了 `<figure>`的内容。

**注意：**从无障碍的角度来说，说明文字和 `alt` 文本扮演着不同的角色。看得见图片的人们同样可以受益于说明文字，而 `alt` 文字只有在图片无法显示时才这样。 所以，说明文字和 `alt` 的内容不应该一样，因为当图片无法显示时，它们会同时出现。

注意 `<figure>` 里不一定要是一张图片，只要是一个这样的独立内容单元：

- 用简洁、易懂的方式表达意图。
- 可以置于页面线性流的某处。
- 为主要内容提供重要的补充说明。

<figure> 可以是几张图片、一段代码、音视频、方程、表格或别的。






## CSS 背景图片

你也可以使用 CSS 把图片嵌入网站中（JavaScript 也行），这个 CSS 属性 [`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image) 和另其他 `background-*` 属性是用来放置背景图片的。比如，为页面中的所有段落设置一个背景图片，你可以这样做：

```css
p {
  background-image: url("images/dinosaur.jpg");
}
```

按理说，这种做法相对于 HTML 中插入图片的做法，可以更好地控制图片和设置图片的位置，那么为什么我们还要使用 HTML 图片呢？

如上所述，CSS 背景图片只是为了装饰 — 如果你只是想要在你的页面上添加一些漂亮的东西，来提升视觉效果，那 CSS 的做法是可以的。但是这样插入的图片完全没有语义上的意义，它们不能有任何备选文本，也不能被屏幕阅读器识别。这就是 HTML 图片有用的地方了。

总而言之，如果图像对您的内容里有意义，则应使用HTML图像。 如果图像纯粹是装饰，则应使用CSS背景图片。  