# 简介

实现一个 ToDo 应用。

- 框架/工具：webpack（4.32.1）+ vue（2.6.10）
- 安装 Vue 的方式： npm

初衷：简化业务逻辑，手动配置 webpack，以实践方式体会前端工程化思想。



# 开发过程记录

**新建项目**

创建项目文件夹，在该文件夹下创建两个基础文件夹：

- src：存放开发时的源代码。
  - assets：存放图片（images）、样式（styles）等资源。
  -  todo ：存放业务逻辑相关代码。
- dist：使用 webpack 打包后代码输出的目标文件夹。最终上传服务器的代码都是从 dist 文件夹下获取。



**配置编辑器**

VSCode

- 插件，加快开发效率
- “文件->首选项->设置”，配置 autoSave 选项为 onFoucsSave。切换文件时自动保存上一个文件。

HBuilderX



**初始化项目**

用 VSCode 打开项目文件夹，然后在 VSCode 中打开该目录下的命令行（终端）。

输入以下命令，初始化为 npm 项目，生成 package.json 文件。

```
npm init
```



**安装第三方库**

运行时依赖：vue

```
npm install vue --save
```

 在本地安装 webpack，接着安装 webpack-cli（此工具用于在命令行中运行 webpack）：

```
npm install webpack webpack-cli --save-dev
```

在 webpack 中使用 vue 需要安装 vue-loader。

```
npm install vue-loader --save-dev
```

某些版本中，vue-loader 可能需要 css-loader 作为第三方依赖。

```
npm install css-loader --save-dev
```

安装好了以后 package.json 多了 devDependencies 属性和 dependencies 属性，里面有包的名字和版本号。

- ^：锁定 1.2.3 的前两位
- ~：锁定 1.2.3 的前一位

package-lock.json 文件存储安装的第三方库的确切版本。也可通过 node_modules 的第三方库的 dist 文件的具体文件查看。

同时在该文件夹中多了一个文件夹 **node_modules，**下载下来的 webpack 和依赖包都在这里。



**编辑代码**

- .vue
- .jsx
- .styl



**配置 webpack** 

创建 webpack.config.js 配置文件，通过这个文件进行 webpack 的配置。

- module.exports = {}
- entry：设置入口文件名（如 index.js、entry.js 等），自行编辑入口文件。
- output：只需设置文件名（如 bundle.[hash:8].js 等），自动生成输出文件。
- module：编辑 rules 数组，配置 test、loader。
  - test：一个正则表达式，用于检测文件类型。
  - loader：处理该文件类型的 loader。
- plugins：内置插件、外置插件
- optimization：chunk
- devServer：开发服务器配置



**编辑入口文件**

- 初始加载页面
- 样式
- 挂载结点
- Vue 对象



**配置 package.json**

只有在这里调用 webpack ，才会使用项目中的 webpack（ devDependencies 中有 webpack 的版本）。在命令行中调用，会使用全局的 webpack。全局的 webpack 与 项目使用 webpack 可能版本不一样。

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config webpack.config.js",
},
```

配置后，在命令行中，`npm run build` 代替了 `webpack` 命令。

webpack 4.0 版本的 build 脚本。

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "cross-env NODE_ENV=production webpack",
    "dev": "cross-env NODE_ENV=development webpack-dev-server --open"
},
```



**打包、发布项目**

`npm run` 执行了 package.json 中的 script 脚本

执行以下命令后，会生成 dist 打包文件夹。把所有依赖打包成一个bundle.js文件，通过代码分割成单元片段并按需加载。

```
npm run build
```

执行以下命令后，浏览器自动打开 `http://localhost:8080/` 页面。

```
npm run dev
```





# 优化

## CSS 单独分离打包

MiniCssExtractPlugin

根据开发环境和打包环境，区分不同的配置。



## 区分打包类库代码以及 hash 优化

区分类库代码和业务逻辑代码。

单独打包 vue 框架。





# 演示