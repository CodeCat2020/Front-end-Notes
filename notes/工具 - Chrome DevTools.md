

# 简介



**九大功能**

- Elements：检查和调整页面，调试 DOM，调试 CSS
- Network：抓包，调试请求，了解页面静态资源分布，网页性能检测，查看请求耗时
- Console ：调试 JavaScript，查看 Console log 日志，交互式代码调试
- Sources ：调试 JavaScript 页面源代码，进行断点调试代码
- Application：查看 & 调试客户端存储，如 Cookie，LocalStorage，SessionStorage 等。
- Performance：查看页面性能细节，细粒度对网页载入进行性能优化。（高阶）
- Memory ：JavaScript CPU 分析器，内存堆分析器。（高阶）
- Security ：查看页面安全及证书问题
- Audits ：使用 Google Lighthouse 辅助性能分析，给出优化建议。（高阶）





**打开方式**

- Chrome 菜单（┇） -> 更多工具 -> 开发者工具

- 在页面元素中右键点击 -> “检查”

- 快捷键（推荐）
  - 打开最近关闭的状态：Cmd +Opt+I (Mac) 或 Ctrl+ Shift+I (Windows)
  - 快速查看 DOM 或样式：Cmd + Opt+C (Mac) 或 Ctrl+ Shift+C (Windows)
  - 快速进入 Console 查看 log 运行 JavaScript : Cmd+ Opt+J (Mac) 或 Ctrl+ Shift+J (Windows)
  - F12



#  Elements 

使用 Elements 调试 DOM

**查看与选择 DOM 节点**

HTML 与 DOM 的区别

在页面中选中 DOM，在 DOM 中反向定位到页面位置

在DOM中检索





**实时编辑 HTML 和 DOM 节点**

编辑内容

- 双击选中，然后修改

编辑属性Attributes

调整 DOM 节点顺序

- 拖拽调整

像编辑器一样编辑 HTML 代码

隐藏/删除/增加/拷贝节点



**在 Console 中访问节点**

使用 document.querySelectAll 访问

使用 $0 快速访问选中的元素

拷贝-> JS Path





**在 DOM 中断点调试**

属性修改时打断点: break on -> attribute modifications

节点删除时打断点: break on -> node removal

子树修改时打断点: break on -> subtree modifications





**调试样式及**2CSS 

**查看与编辑 CSS**



**在元素中动态增加类与伪类**



**快速调试 CSS 数值及颜色图形动画等**





# 使用 Console 和 Sources 调试

**Console 面板简介与交互式命令**

- 运行 JavaScript 代码，交互式编程
- 查看程序中打印的 Log 日志
- 断点调试代码 Debugging







**在 Console 中调试 Log 日志**

console.log 打印信息

console.warn 警告信息

console.error 错误信息

console.table 展示 JSON 格式的复杂信息

console.group 信息组展示

console custom 定制样式

Network 网络请求错误展示



console.time()、console.timeEnd()



### 调试 JavaScript

调试 JavaScript 的基本流程

- 传统的 console.log (甚至 alert() 打印运行时信息调试
- JavaScript 断点调试
  - debugger
- 运行时变量调试，修改源代码临时保存调试







### Sources 面板简介

### 使用 Snippets 来辅助 Debugging

### 使用 DevTools 作为代码编辑器



# Network

### Network 面板简介

- 查看网页资源请求概览,查看资源分布
- 针对单一请求查看 Request/Response 或时间消耗等
- 分析网页性能优化,使用工具代理页面请求数据等



### 使用 Network 详细分析请求



### 使用 Network Waterfall 分析页面载入性能



# Application

### 查看与调试 Cookie







### 查看与调试 LocalStorage 和 SessionStorage







# 调试移动端、H5 页面及远程调试

### 模拟移动设备



### 进行 H5 页面开发





# 集成插件

集成 React 插件



集成 Vue 插件 







# 参考资料

- [Chrome DevTools开发者工具调试指南 - 慕课网课程](https://www.imooc.com/learn/1164)
