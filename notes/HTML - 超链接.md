




# 四、超链接

## 超链接概念

**什么是超链接？**

超链接可以是一个字，一个词，或者一组词，也可以是一幅图像，用户可以点击这些内容来跳转到新的文档或者当前文档中的某个部分。

把鼠标指针移动到网页中的某个链接上，箭头会变为一只小手。

> **提示：**"链接文本" 不必一定是文本。图片或其他 HTML 元素都可以成为链接。



**超链接有什么用？**

HTML 使用超级链接可以与网络上的另一个文档相连。超链接使互联网成为一个互联的网络。

超链接可以链接到文档中的某个部分。用户无须不停地滚动页面来寻找他们需要的信息。

<u>锚点是超链接的一种，又叫命名锚记，可以快速定位当前文档或另一个文档中的某个位置</u>。



**如何创建超链接？**

HTML 使用 `<a>` 标签创建链接。

-  `href` 属性 - 创建指向另一个文档的链接
-  <u>`name` 属性 / `id` 属性 - 创建文档内的书签（锚点），指向当前文档中的某个位置</u>。



## 超链接属性

### **href 属性**

href 属性规定链接的目标。开始标签和结束标签之间的文字被作为超链接来显示。

该属性是可选的，属性值可以是绝对 URL 和相对 URL。

```html
<a href="http://www.w3school.com.cn/">Visit W3School</a>
```

显示：<a href="http://www.w3school.com.cn/">Visit W3School</a>



- 普通超级链接，用于链接网址。

- 下载链接，用于链接特定文档。

  ```html
  <a href="地址\资源名.png">下载图片</a>
  ```

- 电子邮件链接，用于链接到 E- mail。

  ```html
  <a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>
  ```

- 空链接，用于返回页面顶部，有跳转。

  ```html
  <a href＝"#"> ... </a>
  ```

- 锚点跳转，用于跳转到页面某一位置，目前常用于前端路由。

- 用于实现特定的代码功能。

  ```html
  <a href＝"javascrt:void(O);"> ... </a>
  ```

- 页面不跳转的假链接。

  ```html
<a href＝"javascrt:;"> ... </a>
  ```



**电子邮件链接**

使用 `<a>` 和 `mailto:URL` ，打开一个新的电子邮件发送信息。

```html
<a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>
```

显示： <a href="mailto:nowhere@mozilla.org">Send email to nowhere</a>

形式：

- `mailto:`

  邮件地址可选。该形式也会被用户的邮件客户端打开，只是没有收件人的地址信息，通常用在“分享”链接，用户可以发送给他们选择的地址邮件。

- `mailto:link`，链接简单说明收件人的电子邮件地址。

  mailto:nowhere@mozilla.org

- 任何标准的邮件头字段都可以被添加到邮件 URL。其中最常用的是主题(subject)、抄送(cc)和主体(body)。每个字段及其值被指定为查询项。

  - mailto:nowhere@mozilla.org,nobody@mozilla.org
  - mailto:nowhere@mozilla.org?cc=nobody@mozilla.org
  - [mailto:nowhere@mozilla.org?cc=nobody@mozilla.org&subject=This%20is%20the%20subject](mailto:nowhere@mozilla.org?cc=nobody@mozilla.org&subject=This is the subject)

下面是一个包含cc、bcc、主题和主体的示例：

```html
<a href="mailto:nowhere@mozilla.org?cc=name2@rapidtables.com&bcc=name3@rapidtables.com&subject=The%20subject%20of%20the%20email&body=The%20body%20of%20the%20email">
  Send mail with cc, bcc, subject and body
</a>
```

> **注意:** 每个字段的值必须是URL编码的。 也就是说，不能有非打印字符（不可见字符比如制表符、换行符、分页符）和空格 [percent-escaped](http://en.wikipedia.org/wiki/Percent-encoding). 同时注意使用问号（`?`）来分隔主URL与参数值，以及使用&符来分隔`mailto:`中的各个参数。 这是标准的URL查询标记方法。阅读 [The GET method](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Sending_and_retrieving_form_data#The_GET_method) 以了解哪种URL查询标记方法是更常用的。



### **target 属性**

target 定义被链接的文档在何处显示。

```html
<a href="http://www.w3school.com.cn/" target="_blank">Visit W3School!</a>
```

属性值：





| 值              | 描述                                                         |
| :-------------- | :----------------------------------------------------------- |
| **`_blank`**    | **在新窗口中打开**被链接文档。                               |
| `_self`         | 默认值。在相同的框架中打开被链接文档。                       |
| `_parent`       | 在父框架集中打开被链接文档。如果没有 parent 框架或者浏览上下文，与 `self` 相同。 |
| `_top`          | 在整个窗口中打开被链接文档。会清除所有被包含的框架。         |
| ***framename*** | 在指定的框架中打开被链接文档。                               |

a 元素的 target 属性可以指向一个具名的窗口或 iframe



### **name 、id 属性**

name 属性规定锚（anchor）的名称。id 属性可用于创建在一个HTML文档书签标记。

使用 name 或 id 属性可以创建 HTML 页面中的书签。书签不在页面中显示，对用户不可见。

使用命名锚（named anchors）时，可以创建直接跳至该命名锚的链接，链接到 HTML 文档的特定部分（文档片段）。这样使用者就无需不停地滚动页面来寻找需要的信息了。

用法：

首先，在 HTML 文档中对锚进行命名 或 插入 ID（创建一个书签）：

```html
<a name="label">书签</a>
<a id="tips">有用的提示部分</a>
```

然后，在同一个文档中创建指向该锚的链接：

```html
<a href="#label">跳转到书签</a>
<a href="#tips">访问有用的提示部分</a>
```

从一个页面链接到另一个页面文档片段，在 URL 的结尾使用 # 号指向特定的 `id`：

```html
<a href="http://www.w3school.com.cn/html/html_links.asp#label">访问书签</a>
<a href="https://www.runoob.com/html/html-links.html#tips">访问有用的提示部分</a>
```



### **title 属性**

当鼠标指针悬停在链接上时，title 将作为提示信息出现。

```html
<p>I'm creating a link to
<a href="https://www.mozilla.org/en-US/"
   title="The best place to find more information about Mozilla's
          mission and how to contribute">the Mozilla homepage</a>.
</p>
```

I'm creating a link to <a href="https://www.mozilla.org/en-US/"
   title="The best place to find more information about Mozilla's
          mission and how to contribute">the Mozilla homepage</a>.

> 注意：使用键盘来导航网页的人很难获取到标题信息。如果标题信息对于页面非常重要，应该使用所有用户能都方便获取的方式来呈现，例如放在常规文本中。





## 块级链接

可以将一些块级元素转换为链接。

```
<a href="/">         <p>Some Text</p>     </a>
```

例子：将一个图像转换为链接，只需把图像元素放到 `<a>`  `</a>` 标签中间。（img 是行内块级元素）

```html
<a href="https://www.mozilla.org/en-US/">
  <img src="mozilla-image.png" alt="mozilla logo that links to the mozilla homepage">
</a>
```



## URL 和路径

要全面地了解链接目标，需要了解统一资源定位符和文件路径。

统一资源定位符（Uniform Resource Locator，URL）是一个定义了在网络上的位置的一个文本字符串。

URL 使用路径查找文件。路径指定文件所在的位置。

**指向当前目录：**

```html
<p>Want to contact a specific staff member?
Find details on our <a href="contacts.html">contacts page</a>.</p>
```

**指向子目录：**

```html
<p>Visit my <a href="projects/index.html">project homepage</a>.</p>
```

**指向上级目录：**

```html
<p>A link to my <a href="../pdfs/project-brief.pdf">project brief</a>.</p>
```

> 注意：如果需要的话，你可以将这些功能的多个例子和复杂的url结合起来。例如：`../../../complex/path/to/my/file.html`.





## 绝对 URL 和相对 URL

**绝对URL（绝对链接）**： 指向由其在Web上的绝对位置定义的位置，包括协议和域名。不管绝对 URL 在哪里使用，它总是指向确定的相同位置。

**相对URL（相对链接）**： 指向与您链接的文件相关的位置。

例子：

当前文件链接：`http://www.example.com/projects/index.html`，

在 `projects` 的子目录 `pdfs` 中访问到 `project-brief.pdf` 文件。

相对路径：`pdfs/project-brief.pdf`

对应的绝对URL： `http://www.example.com/projects/pdfs/project-brief.pdf`



## 链接的最佳实践

**始终将正斜杠添加到子文件夹**

假如这样书写链接：href="http://www.w3school.com.cn/html"，就会向服务器产生两次 HTTP 请求。这是因为服务器会添加正斜杠到这个地址，然后创建一个新的请求，就像这样：href="http://www.w3school.com.cn/html/"。

**提示：**命名锚经常用于在大型文档开始位置上创建目录。可以为每个章节赋予一个命名锚，然后把链接到这些锚的链接放到文档的上部。如果您经常访问百度百科，您会发现其中几乎每个词条都采用这样的导航方式。

**提示：**假如浏览器找不到已定义的命名锚，那么就会定位到文档的顶端。不会有错误发生。



**用清晰的链接措辞**

好的链接文本：<a href="https://firefox.com/">
  下载Firefox
</a>

```html
<p><a href="https://firefox.com/">
  下载Firefox
</a></p>
```

不好的链接文本：<a href="https://firefox.com/">点击这里</a>下载Firefox

```html
<p><a href="https://firefox.com/">
  点击这里
</a>
下载Firefox</p>
```

- 不要重复 URL 作为链接文本的一部分。
- 不要在链接文本中说“链接”或“链接到”——它只是噪音。
- 链接标签尽可能短。



**尽可能使用相对链接**

当链接到另一个网站时，需要使用绝对链接。但是，当链接到同一网站的其他位置时，应该使用相对链接。

- 首先，检查代码要容易得多——相对 URL 通常比绝对 URL 短得多。
- 其次，在可能的情况下使用相对 URL 更有效。当使用绝对 URL 时，浏览器首先通过DNS 查找服务器的真实位置，然后再转到该服务器并查找所请求的文件。另一方面，相对 URL，浏览器只在同一服务器上查找被请求的文件。因此，如果使用绝对 URL 而不是相对 URL，就会不断地让浏览器做额外的工作，这意味着它的效率会降低。



**链接到非HTML资源 ——留下清晰的指示**

当链接到一个需要下载的资源（如 PDF 文档）或流媒体（如视频或音频）或有另一个潜在的意想不到的效果（打开一个弹出窗口，或加载 Flash 电影），应该添加明确的措辞，以减少任何混乱。

反感例子：

- 在低带宽连接，点击一个链接，然后就开始下载大文件。
- 没有安装 Flash 播放器，点击一个链接，然后突然被带到一个需要 Flash 的页面。

好感例子：

```html
<p><a href="http://www.example.com/large-report.pdf">
  下载销售报告（PDF, 10MB）
</a></p>

<p><a href="http://www.example.com/video-stream/">
  观看视频（将在新标签页中播放, HD画质）
</a></p>

<p><a href="http://www.example.com/car-game">
  进入汽车游戏（需要Flash插件）
</a></p>
```



**在下载链接时使用 download 属性**

当链接到要下载的资源而不是在浏览器中打开时，可以使用 download 属性来提供一个默认的保存文件名（译注：此属性仅适用于[同源URL](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)）。下面是一个下载链接到 Firefox 的 Windows 最新版本的示例：

```html
<a href="https://download.mozilla.org/?product=firefox-latest-ssl&os=win64&lang=en-US"
   download="firefox-latest-64bit-installer.exe">
  Download Latest Firefox for Windows (64-bit) (English, US)
</a>
```






