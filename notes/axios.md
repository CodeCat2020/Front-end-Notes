

# 网络模块封装



## 网络请求模块的选择

Vue 中发送网络请求有非常多的方式那么，在开发中，如何选择呢？

- 选择一：传统的 Ajax （基于 XMLHttpRequest，XHR）。但是配置和调用方式等非常混乱，编码复杂，所以真实开发中很少直接使用，而是使用 jQuery-Ajax。
- 选择二：jQuery-Ajax。相对于传统的 Ajax 非常好用。但是，在 Vue 的整个开发中都是不需要 jQuery。如果为了方便进行一个网络请求而特意引用一个 jQuery 是得不偿失的。（jQuery 的代码 1w+ 行，Vue 的代码才 1w+ 行）。完全没有必要为了用网络请求就引用这个重量级的框架。
- 选择三：Vue1.x 推出了 Vue- resource。Vue-resource 的体积相对于jQuery 小很多，而且是官方退出的。但是，在Vue2.0推出后， Vue 作者就在 GitHub 的 Issues 中说明了去掉vue-resource，并且以后也不会再更新。这意味着以后 vue-reource不再支持新的版本，也不会再继续更新和维护。对以后的项目开发和维护都存在很大的隐患。



为什么要自己封装网络模块？

如果第三方封装的网络模块不维护了，对项目后续的维护是非常麻烦的事情。




在前端开发中，我们一种常见的网络请求方式就是 JSONP。

使用 JSONP 最主要的原因往往是为了解决跨域访问的问题。

JSONP的原理是什么？

- JSONP的核心在于通过 `<script>` 标签的 src 来帮助我们请求数据
- 原因是我们的项目部署在 domain1.com 服务器上时，是不能直接访
  问 domain2.com 服务器上的资料的。
- 这个时候我们利用 `<script>` 标签的 src 帮助我们去服务器请求到数
  据，将数据当做个 javascript 的函数来执行， 并且执行的过程中传
  入我们需要的json。
- 所以封装 jsonp 的核心就在于我们监听 window上的 jsonp 进行回
  调时的名称。



axios 是什么？

Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。







为什么选择 axios？

功能特点：

- 在浏览器中发送 XMLHttpRequests 请求
- 在 node.js 中发送 http 请求
- 支持 Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 XSRF



## axios

### 安装

使用 npm：

```
npm install axios --save
```

使用 bower：

```
bower install axios
```

使用 cdn：

```html
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```



支持多种请求方式：

```
axios(config)
axios.request(config)
axios.get(url[, config])
axios.delete(url[ config])
axios.head(url[ config]) 
axios.post(url[ data[ config])
axios.put(url[, data[, config])
axios.patch(url[ data[ config])
```





有时候我们可能需求同时发送两个请求

- 使用 axiosall，可以放入多个请求的数组。
- axios.all([]) 返回的结果是一个数组 ，使用 axios.spread 可将数组[res1,res2] 展开为 res1, res2







# 参考资料

- axios 中文文档

