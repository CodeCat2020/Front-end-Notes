# 简介

CSS 预处理器用一种专门的编程语言进行 Web 页面样式设计，然后再编译成正常的 CSS 文件，以供项目使用。CSS 预处理器为 CSS 增加一些编程的特性，无需考虑浏览器的兼容性问题。它有层级、mix in 、变量、循环、函数等，具有很方便的 UI 组件模块化开发能力，能极大地提高工作效率。

后处理器（如 PostCSS ）通常被视为在完成的样式表中根据 CSS 规范处理 CSS，让其更有效。目前最常做的是给 CSS 属性添加浏览器私有前缀，解决跨浏览器兼容性的问题。







**预处理器之间的比较**

> [谈谈PostCSS - segmentfault](https://segmentfault.com/a/1190000011595620)

1.变量：

- Sass：使用「$」对变量进行声明，后面紧跟变量名和变量值，变量名和变量值使用冒号进行分割。
- Less：使用「@」对变量进行声明，其余等同 Sass。
- Stylus：声明变量没有任何限定，结尾的分号可有可无，但变量名和变量值之间必须要有『等号』。注意：如果用“@”符号来声明变量，Stylus 会进行编译，但不会赋值给变量。就是说，Stylus 不要使用『@』声明变量。Stylus 调用变量的方法和 Less、Sass 完全相同。

2.**作用域**：

- Sass：三者最差，不存在全局变量的概念。也就是说在 Sass 中定义了相同名字的变量时你就要小心蛋疼了。
- Less：最近的一次更新的变量有效，并且会作用于全部的引用！
- Stylus：Sass 的处理方式和 Stylus 相同，变量值输出时根据之前最近的一次定义计算，每次引用最近的定义有效；

3.嵌套：

- 三种 css 预编译器的「选择器嵌套」在使用上来说没有任何区别，甚至连引用父级选择器的标记 & 也相同。

4.继承：

- Sass 和 Stylus 的继承非常像，能把一个选择器的所有样式继承到另一个选择器上。使用『@extend』开始，后面接被继承的选择器。Stylus 的继承方式来自 Sass，两者如出一辙。
- Less 则又「独树一帜」地用伪类来描述继承关系；

5.导入 @Import：

- Sass 中只能在使用 url() 表达式引入时进行变量插值：

```css
$device: mobile;
@import url(styles.#{$device}.css);
```

- Less 中可以在字符串中进行插值：

```css
@device: mobile;
@import "styles.@{device}.css";
```

- Stylus 中在这里插值不管用，但是可以利用其字符串拼接的功能实现：

```css
device = "mobile"
@import "styles." + device + ".css"
```

总结

- Sass 和 Less 语法严谨，Stylus 相对自由。因为 Less 长得更像 CSS，所以它可能学习起来更容易。
- Sass 和 Compass、Stylus 和 Nib 都是好基友。
- Sass 和 Stylus 都具有类语言的逻辑方式处理：条件、循环等，而 Less 需要通过When等关键词模拟这些功能，这方面 Less 比不上 Sass 和 Stylus。
- Less 在丰富性以及特色上都不及 Sass 和 Stylus，若不是因为 Bootstrap 引入了 Less，可能它不会像现在这样被广泛应用（个人愚见）。







# Sass



# Stylus



# PostCSS



