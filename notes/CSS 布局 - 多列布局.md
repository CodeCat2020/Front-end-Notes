# 多列布局



## 三栏布局 中间自适应

> https://blog.csdn.net/mrchengzp/article/details/78573208



### **绝对定位**

将左右两边使用 absolute 定位，因为绝对定位使其脱离文档流，后面的 center 会自然流动到他们上面，然后使用 margin 属性，留出左右元素的宽度，既可以使中间元素自适应屏幕宽度。

```css
<div class="left">Left</div>
<div class="right">Right</div>
<div class="center">Center</div>
```

```css
.left,.right{ width: 200px;height: 200px; background-color: #ffe6b8;position: absolute;top: 120px;} 
.left{left: 0px;}  
.right{right: 0px;}  
.center{margin:2px 210px;height: 200px;background-color: #eee;}  
```

三个 div 顺序可以任意改变。如果页面上还有其他内容，top 的值需要小心处理，最好能够对样式进行一个初始化。

### **浮动布局**

使用对左右分别使用 float:left 和 float:right，使左右两个元素脱离文档流，中间元素正常在正常文档流中，使用 margin 指定左右外边距对其进行一个定位。

```html
<div class="left">Left</div>
<div class="right">Right</div>
<div class="center">Center</div>
```

```css
.left,.right{ width: 200px;height: 200px; background-color: #ffe6b8 }  
.left {float: left;}  
.right{float: right;}  
.center{margin: 0 210px;height: 200px; background-color: #a0b3d6}  
```

比较简单，兼容性较好，但是浮动元素脱离文档流，需要清除浮动。

受外界影响小，但是三个 div 元素的顺序，center 一定要放在最后。center占据文档流位置，所以一定要放在最后，左右两个元素位置没有关系。当浏览器窗口很小的时候，右边元素会被击倒下一行。

### **圣杯布局**

原理是 margin 负值法。首先需要在 center 元素外部包含一个 div，包含 div 需要设置 float 属性使其形成一个 BFC，并设置宽度，并且这个宽度要和 left 块的 margin 负值进行配合，具体原理[参考这里](http://www.tuicool.com/articles/7n2EZrhttp://)。这里对圣杯布局解释特别详细。

```html
<div id = "wrap">  
    <div id = "center"></div>  
</div>  
<div id = "left_margin"></div>  
<div id = "right_margin"></div>
```

```css
#wrap{ width: 100%;height: 100px; background-color: #fff;float: left;}  
#wrap #center{ margin:0 210px; height: 100px;background-color: #ffe6b8; }  
#left_margin,#right_margin{ float: left;width: 200px;height: 100px;background-color: darkorange }  
#left_margin {margin-left: -100%; background-color: lightpink}  
#right_margin{margin-left: -200px;}  
```

### **Flex 布局**

在外围包裹一层 div，设置为 display:flex；中间一列设置 flex:1；但是盒模型默认紧紧挨着，可以使用 margin 控制外边距。

```html
<div id = "box">  
    <div id = "left_box"></div>  
    <div id = "center_box"></div>  
    <div id = "right_box"></div>  
</div>  
```

```css
#box{width:100%;display: flex; height: 100px;margin: 10px;}  
#left_box,#right_box{width: 200px;height: 100px; margin: 10px; background-color: lightpink}  
#center_box{ flex:1; height: 100px;margin: 10px; background-color: lightgreen} 
```

缺点是不能兼容 IE8 及以下版本。

### **表格布局**

```html
<div class = "table">  
    <div class = "left"></div>  
    <div class = "center"></div>  
    <div class = "right"></div>  
</div> 
```

```css
.table{width: 100%;height: 100px;display: table;}
.table>div{display: table-cell;}
.left{width: 300px;background: red;}
.center{background: yellow;}
.right{width: 300px;background: blue;}
```

当其中一个单元格高度超出的时候，两侧的单元格也是会跟着一起变高的。

### **网格布局**

```html
<div class = "grid">  
    <div class = "left"></div>  
    <div class = "center"></div>  
    <div class = "right"></div>  
</div> 
```

```css
.grid{width:100%;display: grid;grid-template-rows: 100px;grid-template-columns: 300px auto 300px;}
.grid>div{}
.left{width: 300px;background: red;}
.center{background: yellow;}
.right{background: blue;}
```



## 三栏布局 等宽

