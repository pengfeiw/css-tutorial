# css filter属性详解

最近琢磨着把网站主题色更改一下，看到了一篇文章[Dark Mode in One Line of Code](https://davidwalsh.name/dark-mode-invert-filter)，作者讲述了如何用一句代码将网站主题色更改成相反色，这样网站就可以拥有有白天模式和黑夜模式了。
```css
html {
    filter: invert(1);
}
```
使用上面的代码，可以很方便的将页面颜色反转，达到黑夜模式的效果。但是我并不推荐以这种方式去给网站增加黑夜模式，因为这句代码会将页面中的图片的像素颜色也进行反转，所以效果并不是很好。

但是filter属性的确很强大，所以我就在这里介绍一下这个属性。

## 一.语法

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/filter)中是这样描述的：

> The `filter` CSS property applies graphical effects like blur or color shift to an element. Filters are commonly used to adjust the rendering of images, backgrounds, and borders.

翻译过来就是，`filter`属性可以为元素添加模糊或颜色偏移等图形效果。一般用来调整图片、背景和边框的渲染。

具体语法如下：
```css
filter: <filter-function> [<filter-function>]* | none
```
filter函数有：`grayscale`、`blur`、`sepia`、`saturate`、`opacity`、`brightness`、`contrast`、`hue-rotate`和`invert`。大部分函数的参数范围为0-1数字之间，其中`blur`函数参数为任意数字后接`px`单位，`hue-rotate`函数参数为一个整数后接`deg`单位。

## 二.filter函数

### grayscale

`grayscale`用于调整元素的灰度值。参数范围为0-1，0表示无效果，1表示灰度最大。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: grayscale" src="https://codepen.io/AhCola/embed/XWRxMew?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/XWRxMew">
  css filter: grayscale</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: grayscale(1)`。

### blur

`blue`用于调整图片模糊度的。参数为大于0的数字，后接`px`单位。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: blur" src="https://codepen.io/AhCola/embed/BaRqWJm?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/BaRqWJm">
  css filter: blur</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: blur(5px)`。

### sepia

`sepia`用于调整元素的褐色程度。参数范围为0-1。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: sepia" src="https://codepen.io/AhCola/embed/vYmVxRg?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/vYmVxRg">
  css filter: sepia</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: sepia(1)`。

### saturate

调整元素的饱和度。参数范围为0-1。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: saturate" src="https://codepen.io/AhCola/embed/ExmdWLY?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/ExmdWLY">
  css filter: saturate</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: saturate(0)`，第二张图片`filter: saturate(1)`，饱和度为0与灰度值为1效果类似。

### opacity

调整元素的透明度。参数范围为0-1，0表示完全透明，1表示完全不透明。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: opacity" src="https://codepen.io/AhCola/embed/eYWPvKa?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/eYWPvKa">
  css filter: opacity</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: opacity(0.2)`，第二张图片`filter: opacity(1)`。css也有一个[opacity](https://developer.mozilla.org/zh-CN/docs/Web/CSS/opacity)属性可以调整元素透明度，用法一样。

### brightness

`brightness`用于调整元素的亮度。范围为0-1，0表示全黑，1表示最亮。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: brightness" src="https://codepen.io/AhCola/embed/MWmPpqR?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/MWmPpqR">
  css filter: brightness</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: brightness(0)`，显示为黑色。

### contrast

调整元素的对比度。默认值为1，表示与原图一致，取值小于1时，对比度降低，取值大于1时表示对比度增大。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: contrast" src="https://codepen.io/AhCola/embed/qBmJrQZ?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/qBmJrQZ">
  css filter: contrast</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

图片一`filter: contrast(0.2)`，图片二`filter: contrast(3)`，图片三为默认值1。

### hue-rotate

色相旋转，取值为角度值，单位为`deg`。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter: hue-rotate" src="https://codepen.io/AhCola/embed/wvdYJRj?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/wvdYJRj">
  css filter: hue-rotate</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: hue-rotate(40deg)`。

### invert

将元素的颜色反转。参数范围为0-1，默认值为0。

<iframe height="300" style="width: 100%;" scrolling="no" title="css filter:  invert" src="https://codepen.io/AhCola/embed/ExmdWJj?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/ExmdWJj">
  css filter:  invert</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

第一张图片`filter: invert(1)`。


（完）
