# JavaScript 模块化

## 概述

JavaScript 对模块化的现实需要

- JS 设计之初，主要用于处理简单的页面效果和逻辑验证之类的简单工作。只需要少量的代码就可以完成这些功能。
- 被过于随意的设计，缺乏模块化一直是其缺陷之一。
- 随着单页应用与富客户端的流行，需要使用 JavaScript 处理越来越多的事情，以前许多本来由后台处理的内容都转移到前端来处理，这使代码量急剧膨胀。
- 不断增长的代码库也急需合理的代码分割与依赖管理的解决方案，这就是我们在软件工程领域所熟悉的模块化。
- 同时在开发中，难免会需要一些“轮子”，如果没有模块（ Model ）这个概念， 我们将很难简便地使用别人制造的“轮子” 。
- 模块化主要解决的问题：解决代码分割、增强维护性、提高代码重用、作用域隔离、模块之间的依赖管理、发布的自动化打包与处理等多个方面。



为什么要使用模块化？举例说明

- 团队开发项目时，JavaScript 同名全局变量和 `<script>` 顺序带来的问题。
- 闭包引起代码不可复用。
- 自己实现简单的模块化
- 模块化规范



## 历史

主要的模块化方案

- 直接声明依赖（Directly Defined Dependences）
- 命名空间（Namespace Pattern）
- 模块模式（Module Pattern）
- 依赖分离定义（Detached Dependency Definitions）
- 沙盒（Sandbox）
- 依赖注入（Dependency Injection）
- 标签化模块（Labeled Modules）
- CommonJS、AMD、UMD、ES 2015 Modules、CMD



**1. 直接声明依赖**

除了备注描述，什么问题都没解决

```js
// file app.js
var helloInLang = {
  en: 'Hello world!'
};

// file hello.js

/* helloInLang defined in app.js */
function writeHello(lang) {
  document.write(helloInLang[lang]);
};
```

**2. 命名空间**

命名空间模式始于 2002 年，使用特殊的约定命名，用于避免命名冲突和全局作用域污染。

缺点：大型项目可维护性较差，没有解决模块间依赖管理的问题。

```js
// file app.js
var app = {};

// file greeting.js
app.helloInLang = {
  en: 'Hello world!'
};

// file hello.js
app.writeHello = function (lang) {
  document.write(app.helloInLang[lang]);
};
```

**3. 模块模型**

封装了变量和 function，和全局的 namaspace 不接触，松耦合

只暴露可用 public 的方法，其它私有方法全部隐藏

```js
// file app.js
var app = {};

// file greeting.js
app = (function (app) {
    var _app = app || {};

    _app.helloInLang = {
      en: 'Hello world!'
    };

    return _app;
} (app));

// file hello.js
app = (function (app) {
    var _app = app || {};

    _app.writeHello = function (lang) {
      document.write(app.helloInLang[lang]);
    };

    return _app;
} (app));
```

**4. 依赖注入**

2009 年 Angular 引入 Java 的依赖注入思想。

核心思想：某个模块不需要手动初始化某个依赖对象，只需要声明该依赖，并由外部框架自动实例化该对象，并传递到模块内。

```js
// file greeting.js
angular.module('greeter', [])
  .value('greeting', {
    helloInLang: {
      en: 'Hello world!'
    },
    ayHello: function(lang) {
      return this.helloInLang[lang];
    }
  });

// file app.js
angular.module('app', ['greeter'])
  .controller('GreetingController', ['$scope', 'greeting', function($scope, greeting) {
    $scope.phrase = greeting.sayHello('en');
  }]);
```

**5. CommonJS**

服务器端 javascript 模块化解决方案，适用于同步模块加载。

```js
// file greeting.js
var helloInLang = {
    en: 'Hello world!'
};
var sayHello = function (lang) {
    return helloInLang[lang];
}
module.exports.sayHello = sayHello;

// file hello.js
var sayHello = require('./lib/greeting').sayHello;
var phrase = sayHello('en');
console.log(phrase);
```

**6. AMD**

浏览器端 javascript 模块化解决方案，适用于异步模块加载。

```js
// file lib/greeting.js
define(function() {
    var helloInLang = {
        en: 'Hello world!'
    };

    return {
        sayHello: function (lang) {
            return helloInLang[lang];
        }
    };
});

// file hello.js
define(['./lib/greeting'], function(greeting) {
    var phrase = greeting.sayHello('en');
    document.write(phrase);
});
```

**7. UMD**

UMD 允许在环境中同时使用 AMD 与 CommonJS 规范。

```js
(function(define) {
    define(function () {
        var helloInLang = {
            en: 'Hello world!'
        };

        return {
            sayHello: function (lang) {
                return helloInLang[lang];
            }
        };
    });
}(
    typeof module === 'object' && module.exports && typeof define !== 'function' ?
    function (factory) { module.exports = factory(); } :
    define
));复制代码
```

**8. ES2015 Modules**

ES2015 Modules 作为 JavaScript 官方标准，日渐成为了开发者的主流选择。

```js
// file lib/greeting.js
const helloInLang = {
    en: 'Hello world!'
};

export const greeting = {
    sayHello: function (lang) {
        return helloInLang[lang];
    }
};

// file hello.js
import { greeting } from "./lib/greeting";
const phrase = greeting.sayHello("en");
document.write(phrase);复制代码
```



**9. CMD**



# JavaScript 模块化规范



- CommonJS：主要是服务器端规范（比如 Node.js） 。
- AMD：客户端规范。**推崇依赖前置**，实现主要有 require.js。
- CMD：客户端规范。**推崇依赖就近**，主要实现有 SeaJS，但是已经停止维护了。
- UMD
- ECMAScript 6 Module 。随着 ES 6 的普及，第三方的模块化规范的实现将会慢慢地被淘汰。





相似点：

模块化有两个核心：导出和导入



## CommonJS





CommonJS 是服务器端模块的规范， Node.js 采用了这个规范。CommonJS 规范同步加载模块，也就是说，只有加载完成，才能执行后面的操作。





**定义模块**

一个单独的文件就是一个模块，文件中的作用域独立，文件中定义的变量无法被其他文件引用。如果需要使用这些变量，需要将其定义为全局变量（不建议）。

**输出模块**（导出）

模块只有一个接口对象，使用 `module.exports` 对象可以将需要输出的内容放入到该对象中。

```js
module.exports = {
	flag: true,
    test(a, b) {
        return a + b
    },
}
```

**加载模块**（导入）

通过 require 加载，例如 `var module = require('./moduleFile.js')` ，该module 的值对应文件内部的 `module.exports` 对象，然后就可以通过 module 名称引用模块中暴露的接口变量或接口函数了。

```js
// CommonJS 模块
let {test,flag} = require('./moduleFile.js')
// 等同于
let _MA = require('./moduleFile.js')
let test = _MA.test
let flag = _MA.flag
```









## AMD

AMD 规范则非同步加载模块，允许指定回调函数。





## CMD





## UMD



## ES6 Module







## 比较







# 参考资料

- http://www.commonjs.org/










