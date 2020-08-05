# Cookie





## 定义

HTTP 协议是无状态的，协议对于发送过的请求或响应都不做持久化处理。这是为了更快地处理大量事务，确保协议的可伸缩性，而特意把 HTTP 协议设计成如此简单的。

可是，随着 Web 的不断发展，因无状态而导致业务处理变得棘手的情况增多了。比如，某些情况下需要保存用户登录状态。

HTTP/1.1 引入 Cookie 来保存状态信息。  

Cookie 是服务器发送到用户浏览器并保存在本地的一小块数据，**它会在浏览器之后向同一服务器再次发起请求时被携带上**，用于告知服务端两个请求是否来自同一浏览器。由于之后每次请求都会需要携带 Cookie 数据，因此会带来额外的性能开销（尤其是在移动环境下）。

Cookie 曾一度用于客户端数据的存储，因为当时并没有其它合适的存储办法而作为唯一的存储手段，但现在随着现代浏览器开始支持各种各样的存储方式，Cookie 渐渐被淘汰。新的浏览器 API 已经允许开发者直接将数据存储到本地，如使用 Web storage API（本地存储和会话存储）或 IndexedDB。





客户端设置 cookie 与服务端设置 cookie 有什么区别？

无论是客户端还是服务端，都只能向自己的域或更高级域设置 cookie。

服务端可以设置 `httpOnly: true`，带有该属性的 Cookie 客户端无法读取。

客户端只会带上与请求同域的 cookie，例如 `client.com/index.html` 会带上 `client.com` 的 cookie， `server.com/app.js`会带上`server.com`的cookie，并且也会带上 httpOnly 的 cookie。

但是，如果是向服务端的 Ajax 请求，则不会带上cookie。



## 携带问题



**同域/跨域 Ajax 请求到底会不会带上 cookie？**

fetch 在默认情况下, 不管是同域还是跨域 Ajax 请求都不会带上 cookie。只有当设置了 `credentials` 时才会带上该 Ajax 请求所在域的 cookie，服务端需要设置响应头 `Access-Control-Allow-Credentials: true`，否则浏览器会因为安全限制而报错，拿不到响应。

credentials 属性值：

- include：跨域 Ajax 带上 cookie。
- same-origin：仅同域 Ajax 带上 cookie。
- omit：任何情况都不带 cookie。

**fetch 设置凭据**

```js
fetch(url, {
    credentials: "include", // include, same-origin, omit
})
```

axios 和 jQuery 在同域 Ajax 请求时会带上 cookie，跨域请求不会，跨域请求需要设置 `withCredentials` 和服务端响应头。`withCredentials`指示是否应使用凭据发出跨站点访问控制请求，默认 false。

**使 axios 带上 cookie**

```js
axios.get('http://server.com', {withCredentials: true})
```

**jQuery 设置 withCredentials**

```js
$.ajax({
    method: 'get',
    url: 'http://server.com',
    xhrFields: {
        withCredentials: true
    }
})
```





## 用途

- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
- 个性化设置（如用户自定义设置、主题等）
- 浏览器行为跟踪（如跟踪分析用户行为等）

## 创建过程

**Cookie 的生成**

服务器如果希望在浏览器保存 Cookie，就要在 HTTP 回应的头信息里面，放置一个 `Set-Cookie` 字段。客户端得到响应报文后把 Cookie 内容保存到浏览器中。

HTTP 回应可以包含多个 `Set-Cookie` 字段。一个 `Set-Cookie` 字段里面，可以同时包括多个属性，没有次序的要求。

```html
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly

[page content]
```

上面代码会在浏览器保存两个 Cookie：名为 `yummy_cookie` 的 Cookie，值为 `choco`；名为 `tasty_cookie` 的 Cookie，值为 `strawberry`。



如果服务器想改变一个早先设置的 Cookie，必须同时满足四个条件：Cookie 的 `key`、`domain`、`path` 和 `secure` 都匹配。

举例来说，如果原始的 Cookie 是用如下的`Set-Cookie`设置的。

```
Set-Cookie: key1=value1; domain=example.com; path=/blog
```

改变上面这个 Cookie 的值，就必须使用同样的 `Set-Cookie`。

```
Set-Cookie: key1=value2; domain=example.com; path=/blog
```

只要有一个属性不同，就会生成一个全新的 Cookie，而不是替换掉原来那个 Cookie。

```
Set-Cookie: key1=value2; domain=example.com; path=/
```

上面的命令设置了一个全新的同名 Cookie，但是 `path` 属性不一样。下一次访问`example.com/blog` 的时候，浏览器将向服务器发送两个同名的 Cookie。

```
Cookie: key1=value1; key1=value2
```



**Cookie 的发送**

客户端之后对同一个服务器发送请求时，会从浏览器中取出 Cookie 信息并通过 Cookie 请求首部字段发送给服务器。

`Cookie` 字段可以包含多个 Cookie，使用分号（`;`）分隔。

```html
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie=choco; tasty_cookie=strawberry
```

服务器收到浏览器发来的 Cookie 时，有两点是无法知道的。

- Cookie 的各种属性，比如何时过期。
- 哪个域名设置的 Cookie，到底是一级域名设的，还是某一个二级域名设的。



## 字段



**name**：唯一确定 cookie 的名称。不区分大小写，实践中最好看作是区分大小写的，因为某些服务器会这样处理 cookie。cookie 的名称必须是经过 URL 编码的。

**value**：储存在cookie 中的字符串值。值必须被 URL 编码。



### Domain, Path

`Domain` 标识指定了哪些主机可以接受 Cookie。如果不指定，默认为当前文档的主机（不包含子域名）。比如，`example.com` 不设置 Cookie 的 `domain` 属性，那么 `sub.example.com `将不会附带这个 Cookie。

如果指定了 `Domain` ，则一般包含子域名。例如，如果设置 Domain=mozilla.org，则 Cookie 也包含在子域名中（如 developer.mozilla.org）。

如果服务器指定的域名不属于当前域名，浏览器会拒绝这个 Cookie。

- 非顶级域名（比如，二级域名或者三级域名），设置的 cookie 的 domain 只能为顶级域名或者二级域名或者三级域名本身，不能设置其他二级域名的 cookie，否则 cookie无法生成。
- 顶级域名只能设置 domain 为顶级域名，不能设置为二级域名或者三级域名，否则cookie 无法生成。要想 cookie 在多个二级域名中共享，需要设置 domain 为顶级域名。

`Path` 属性指定浏览器发出 HTTP 请求时，哪些路径要附带这个 Cookie。（该 URL 路径必须存在于请求 URL 中）。只要浏览器发现，`Path` 属性是 HTTP 请求路径的开头一部分，就会在头信息里面带上这个 Cookie。以字符 %x2F ("/") 作为路径分隔符，子路径也会被匹配。例如，设置 Path=/docs，则以下地址都会匹配：

- /docs
- /docs/Web/
- /docs/Web/HTTP



浏览器的同源政策规定，两个网址只要域名相同和端口相同，就可以共享 Cookie。



**能设置或读取子域的 cookie 吗？**

不能。只能向当前域或更高级域设置或读取 Cookie。

例如 `client.com` 不能向 `a.client.com` 设置 cookie，而 `a.client.com`  可以向 `client.com` 设置 cookie。



### **Expires / Max-Age**

`Expires` 属性指定一个具体的到期时间，到了指定时间以后，浏览器就不再保留这个 Cookie。它的值是 UTC 格式（Wdy, DD-Mon-YYYY HH:MM:SS GMT），可以使用 `Date.prototype.toUTCString()` 进行格式转换。

```
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

另外，浏览器根据本地时间，决定 Cookie 是否过期，由于本地时间是不精确的，所以没有办法保证 Cookie 一定会在服务器指定的时间过期。

`Max-Age` 属性指定从现在开始 Cookie 存在的秒数，比如 `60 * 60 * 24 * 365`（即一年）。过了这个时间以后，浏览器就不再保留这个 Cookie。

如果同时指定了 `Expires` 和 `Max-Age`，那么 `Max-Age` 的值将优先生效。

如果 `Set-Cookie` 字段没有指定 `Expires` 或 `Max-Age` 属性 或 `Expires` 设为 `null`，那么这个 Cookie 就是 Session Cookie，即它只在本次对话存在，一旦用户关闭浏览器，浏览器就不会再保留这个 Cookie。









### HttpOnly

标记为 `HttpOnly` 的 Cookie 不能被 JavaScript 脚本调用，主要是`document.cookie` 属性、`XMLHttpRequest` 对象和 Request API 都拿不到该属性。这样就防止了该 Cookie 被脚本读到，只有浏览器发出 HTTP 请求时，才会带上该 Cookie。

跨站脚本攻击 (XSS) 常常使用 JavaScript 的 `document.cookie` API 窃取用户的 Cookie 信息，因此使用 HttpOnly 标记可以在一定程度上避免 XSS 攻击。

```html
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```



### Secure

标记为 `Secure` 的 Cookie 只能通过被 HTTPS 协议加密过的请求发送给服务端。如果当前协议是 HTTP，浏览器会自动忽略服务器发来的 `Secure` 属性。该属性只是一个开关，不需要指定值。如果通信是 HTTPS 协议，该开关自动打开。

但即便设置了 Secure 标记，敏感信息也不应该通过 Cookie 传输，因为 Cookie 有其固有的不安全性，Secure 标记也无法提供确实的安全保障。



### SameSite

Chrome 51 开始，浏览器的 Cookie 新增加了一个 `SameSite` 属性，用来防止 CSRF 攻击和用户追踪。

Cookie 往往用来存储用户的身份信息，恶意网站可以设法伪造带有正确 Cookie 的 HTTP 请求，这就是 CSRF 攻击。举例来说，用户登陆了银行网站 `your-bank.com`，银行服务器发来了一个 Cookie。

```
Set-Cookie:id=a3fWa;
```

用户后来又访问了恶意网站 `malicious.com`，上面有一个表单。

用户一旦被诱骗发送这个表单，银行网站就会收到带有正确 Cookie 的请求。为了防止这种攻击，表单一般都带有一个随机 token，告诉服务器这是真实请求。

```html
<form action="your-bank.com/transfer" method="POST">
  <input type="hidden" name="token" value="dad3weg34">
  ...
</form>
```

这种第三方网站引导发出的 Cookie，就称为第三方 Cookie。它除了用于 CSRF 攻击，还可以用于用户追踪。比如，Facebook 在第三方网站插入一张看不见的图片。

```html
<img src="facebook.com" style="visibility:hidden;">
```

浏览器加载上面代码时，就会向 Facebook 发出带有 Cookie 的请求，从而 Facebook 就会知道你是谁，访问了什么网站。

Cookie 的 `SameSite` 属性用来限制第三方 Cookie，从而减少安全风险。它可以设置三个值。

- Strict：最为严格，完全禁止第三方 Cookie。过于严格，可能造成非常不好的用户体验。

  ```
  Set-Cookie: CookieName=CookieValue; SameSite=Strict;
  ```

- Lax：稍稍放宽，大多数情况也是不发送第三方 Cookie，但是导航到目标网址的 Get 请求除外。导航到目标网址的 GET 请求，只包括三种情况：链接，预加载请求，GET 表单。

  ```
  Set-Cookie: CookieName=CookieValue; SameSite=Lax;
  ```


- None：Chrome 计划将 `Lax` 变为默认设置。这时，网站可以选择显式关闭 `SameSite` 属性，将其设为 `None`。不过，前提是必须同时设置 `Secure` 属性（Cookie 只能通过 HTTPS 协议发送），否则无效。

  下面的设置无效。

  ```
  Set-Cookie: widget_session=abc123; SameSite=None
  ```

  下面的设置有效。

  ```
  Set-Cookie: widget_session=abc123; SameSite=None; Secure
  ```

设置了 `Strict` 或 `Lax` 以后，基本就杜绝了 CSRF 攻击。









## 分类

- 会话期 Cookie：浏览器关闭之后它会被自动删除，也就是说它仅在会话期内有效。
- 持久性 Cookie：指定过期时间（Expires）或有效期（max-age）之后就成为了持久性的 Cookie。

```html
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```



## document.cookie

`document.cookie` 属性用于读写当前网页的 Cookie。

**读取**

读取的时候，它会返回当前网页的所有 Cookie，前提是该 Cookie 不能有 `HTTPOnly` 属性。

```js
document.cookie = "yummy_cookie=choco";
document.cookie = "tasty_cookie=strawberry";
console.log(document.cookie);	
// yummy_cookie=choco;tasty_cookie=strawberry
```

多个 Cookie 之间用分号隔开。必须手动还原，才能取出每一个 Cookie 的值。

```js
var cookies = document.cookie.split(';');
for (var i = 0; i < cookies.length; i++) {
  console.log(cookies[i]);
}
// yummy_cookie=choco
// tasty_cookie=strawberry
```

**写入**

`document.cookie` 属性是可写的，可以通过它为当前网站添加 Cookie。写入的时候，Cookie 的值必须写成 `key=value` 的形式，等号两边不能有空格。

但是，`document.cookie` 一次只能写入一个 Cookie，而且写入并不是覆盖，而是添加。

另外，写入 Cookie 的时候，必须对分号、逗号和空格进行转义（它们都不允许作为 Cookie 的值），这可以用 `encodeURIComponent` 方法达到。

```
document.cookie = 'test1=hello; expires=Fri, 31 Dec 2020 23:59:59 GMT';
document.cookie = 'test2=world';
document.cookie
// test1=hello;test2=world
```

`document.cookie` 读写行为的差异（一次可以读出全部 Cookie，但是只能写入一个 Cookie），与 HTTP 协议的 Cookie 通信格式有关。浏览器向服务器发送 Cookie 的时候，`Cookie` 字段是使用一行将所有 Cookie 全部发送；服务器向浏览器设置 Cookie 的时候，`Set-Cookie` 字段是一行设置一个 Cookie。

各个属性的写入注意点如下。

- `path` 属性必须为绝对路径，默认为当前路径。
- `domain` 属性值必须是当前发送 Cookie 的域名的一部分。比如，当前域名是 `example.com`，就不能将其设为 `foo.com`。该属性默认为当前的一级域名（不含二级域名）。
- `max-age` 属性的值为秒数。
- `expires` 属性的值为 UTC 格式，可以使用`Date.prototype.toUTCString()` 进行日期格式转换。

`document.cookie`写入 Cookie 的例子如下。

```js
document.cookie = 'fontSize=14; '
  + 'expires=' + someDate.toGMTString() + '; '
  + 'path=/subdirectory; '
  + 'domain=*.example.com';
```

Cookie 的属性一旦设置完成，就没有办法读取这些属性的值。

删除一个现存 Cookie 的唯一方法，是设置它的 `expires` 属性为一个过去的日期。

```js
document.cookie = 'fontSize=;expires=Thu, 01-Jan-1970 00:00:01 GMT';
```





## 限制

> 《JavaScript 高级程序设计》Ch23.3.1

由于cookie 是存在客户端计算机上的，还加入了一些限制确保 cookie 不会被恶意使用，同时不会占据太多磁盘空间。

每个域的 cookie 总数是有限的，不过浏览器之间各有不同。

- IE6 以及更低版本限制每个域名最多 20 个 cookie。

- IE7 和之后版本每个域名最多 50 个。IE7 最初是支持每个域名最大 20 个cookie，之后被微软的一个补丁所更新。

- Firefox 限制每个域最多 50 个 cookie。

- Opera 限制每个域最多 30 个 cookie。

- Safari 和 Chrome 对于每个域的 cookie 数量限制没有硬性规定。

当超过单个域名限制之后还要再设置 cookie，浏览器就会清除以前设置的 cookie。

- IE 和 Opera 会删除最近最少使用过的（LRU，Least Recently Used）cookie，腾出空间给新设置的 cookie。
- Firefox 随机决定要清除哪个cookie，所以考虑 cookie 限制非常重要，以免出现不可预期的后果。

浏览器中对于 cookie 的尺寸也有限制。大多数浏览器都有大约 4096 字节（加减1）的长度限制。为了最佳的浏览器兼容性，最好将整个 cookie 长度限制在 4095 字节（含 4095）以内。尺寸限制影响到一个域下所有的 cookie，而并非每个 cookie 单独限制。

如果尝试创建超过最大尺寸限制的 cookie，那么该 cookie 会被悄无声息地丢掉。注意，虽然一个字符通常占用一字节，但是多字节情况则有不同。

IE 提供了一种存储方式，可以持久化用户数据，叫作 userdata ，从 IE5 就开始支持。每个数据最多 128KB ， 每个域名下最多 1MB 。这个持久化数据放在缓存中， 如果缓存没有清理，那么会一直存在。





# Session

除了可以将用户信息通过 Cookie 存储在用户浏览器中，也可以利用 Session 存储在服务器端，存储在服务器端的信息更加安全。

Session 可以存储在服务器上的文件、数据库或者内存中。也可以将 Session 存储在 Redis 这种内存型数据库中，效率会更高。



使用 Session 维护用户登录状态的过程如下：

- 用户进行登录时，用户提交包含用户名和密码的表单，放入 HTTP 请求报文中；
- 服务器验证该用户名和密码，如果正确则把用户信息存储到 Redis 中，它在 Redis 中的 Key 称为 Session ID；
- 服务器返回的响应报文的 Set-Cookie 首部字段包含了这个 Session ID，客户端收到响应报文之后将该 Cookie 值存入浏览器中；
- 客户端之后对同一个服务器进行请求时会包含该 Cookie 值，服务器收到之后提取出 Session ID，从 Redis 中取出用户信息，继续之前的业务操作。

应该注意 Session ID 的安全性问题，不能让它被恶意攻击者轻易获取，那么就不能产生一个容易被猜到的 Session ID 值。此外，还需要经常重新生成 Session ID。在对安全性要求极高的场景下，例如转账等操作，除了使用 Session 管理用户状态之外，还需要对用户进行重新验证，比如重新输入密码，或者使用短信验证码等方式。



## 浏览器禁用 Cookie

Cookie 与 Session，一般认为是两个独立的东西，Session 采用的是在服务器端保持状态的方案，而 Cookie 采用的是在客户端保持状态的方案。

为什么禁用 Cookie 就不能得到 Session？因为 Session 是用 Session ID 来确定当前对话所对应的服务器 Session，而 Session ID 是通过 Cookie 来传递的，禁用 Cookie 相当于失去了 Session ID，也就得不到 Session了。

假定用户关闭 Cookie 的情况下使用 Session，其实现途径有以下几种：

- 设置php.ini配置文件中的“session.use_trans_sid = 1”，或者编译时打开打开了“--enable-trans-sid”选项，让PHP自动跨页传递Session ID。
- 使用 URL 重写技术，将 Session ID 作为 URL 的参数进行传递。手动通过 URL 传值、隐藏表单传递 Session ID。

- 用文件、数据库等形式保存 Session ID，在跨页过程中手动调用。



## Cookie 与 Session 选择

相同点：

- Cookie 和 Session 都是用来跟踪浏览器用户身份的会话方式
- Session、Cookie 都有失效时间，过期后会自动删除，减少系统开销。
- Session 和 Cookie 不能跨窗口使用，每打开一个浏览器系统会赋予一个SessionID，此时的 SessionID 不同，若要完成跨浏览器访问数据，可以使用 Application。

两者的应用场景不太一样。不同之处：

- 存储位置：Cookie 数据保存在客户端（浏览器端），Session 数据保存在服务器端。

- 存储的多样性：Session 可以存储在 Redis 中、数据库中、应用程序中；而 Cookie 只能存储在浏览器中。

- 用户可以通过浏览器设置决定是否保存 Cookie，而不能决定是否保存Session，因为 Session 是由服务器端维护的。

- 容量和个数限制：Cookie 有容量限制，单个 Cookie 保存的数据不能超过4K。每个站点下的 Cookie 也有个数限制，很多浏览器都限制一个站点最多保存 20 个 Cookie。Session 存储容量大小没有限制。但是为了服务器性能考虑，一般不能存放太多数据。

- 存取方式：Cookie 只能存储 ASCII 码字符串，而 Session 则可以存储任何类型的数据，因此在考虑数据复杂性时首选 Session。

- 隐私策略：Cookie 存储在客户端中，容易被恶意查看，可以被伪造和修改，他人可以分析存放在本地的 Cookie 并进行 Cookie 欺骗。如果非要将一些隐私数据存在 Cookie 中，可以将 Cookie 值进行加密，然后在服务器进行解密；而 Session 存储在服务器上，对客户端是透明的，不存在敏感信息泄露的风险。

- **有效期**：Cookie 可以长期存储，只要不超过设置的过期时间，可以一直存储。Session 在超过一定的操作时间（通常为30分钟）后会失效，但是当关闭浏览器时，为了保护用户信息，会自动调用session.invalidate() 方法，该方法会清除掉 Session 中的信息。

  Session 依赖于名为 JSESSIONID 的 Cookie，而 Cookie JSESSIONID 的过期时间默许为 –1，只需关闭了阅读器该 Session 就会失效。运用 URL 地址重写也不能完成。而且假如设置 Session 的超时时间过长，服务器累计的 Session 就会越多，越容易招致内存溢出。

- 服务器压力：Cookie保管在客户端，不占用服务器资源。Session是保管在服务器端的，每个用户都会产生一个Session。假如并发访问的用户十分多，Cookie 是很好的选择。关于 Google、Baidu、Sina 来说，Cookie 或许是唯一的选择。

  对于大型网站，如果用户所有的信息都存储在 Session 中，那么开销是非常大的，因此不建议将所有的用户信息都存储到 Session 中。

- **浏览器支持**：Cookie是需要浏览器支持。假如浏览器不支持 Cookie，需要运用 Session 以及 URL 地址重写。

  假如客户端支持 Cookie，则 Cookie 既能够设为本浏览器窗口以及子窗口内有效（把过期时间设为–1），也能够设为一切阅读器窗口内有效（把过期时间设为某个大于0的整数）。但Session只能在本阅读器窗口以及其子窗口内有效。假如两个浏览器窗口互不相干，它们将运用两个不同的Session。（IE8下不同窗口Session相干）

- **跨域支持**：Cookie 支持跨域名访问，例如，所有 a.com 的 Cookie 在 a.com 下都能用。而 Session 则不会支持跨域名访问，例如，www.a.com 的 Session 在 api.a.com 下不能用。

仅运用 Cookie 或者仅运用 Session 可能完成不了理想的效果。这时应该尝试一下同时运用 Cookie 与 Session。Cookie 与 Session 的搭配运用在实践项目中会完成很多意想不到的效果。











# 参考资料

- [阮一峰：Cookie](https://wangdoc.com/javascript/bom/cookie.html#cookie-%E4%B8%8E-http-%E5%8D%8F%E8%AE%AE)
- [Cookie的设置，读取以及是否自动携带问题 - 掘金](https://juejin.im/post/5b5df0aee51d451998415485)