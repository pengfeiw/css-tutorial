# z-index和栈空间

*本节内容，将深入研究z-index这个属性和栈空间（stacking context）。*

## 一.z-index
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)上是这样描述z-index的：
> `z-index`属性设定了一个定位元素及其后代元素或flex项目的z-order。 当元素之间重叠的时候，`z-index`较大的元素会覆盖较小的元素在上层进行显示。

MDN中还提到了下面两点内容，作为补充。
> 1.盒子在当前堆叠上下文中的堆叠层级。
>
> 2.盒子是否创建一个本地堆叠上下文。

如果你足够细心，应该能够注意到**堆叠上下文**这个词。本着好好学习天天向上的精神，我们来个追查到底。

先来看一个例子。
<iframe height="300" style="width: 100%;" scrolling="no" title="z-index  and stacking context_01" src="https://codepen.io/AhCola/embed/WNjVEBm?default-tab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/AhCola/pen/WNjVEBm">
  z-index  and stacking context_01</a> by Pengfei Wang (<a href="https://codepen.io/AhCola">@AhCola</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

为什么`z-index`设置为`-1`，但是它还是在最上面显示呢？

其实罪魁祸首就是**堆叠上下文**。

## 二.栈空间

**栈空间（stacking context），也称堆叠上下文**。[w3c](https://www.w3.org/TR/2012/WD-css3-positioning-20120207/#det-stacking-context)中有详细介绍，我在这里就扮演一个搬运工的角色，将这部分内容搬出来。

在css（html）的世界中，所有的元素都是处于三维世界中的，对的是三维的，它们不仅仅只有x和y坐标，还有一个z坐标，在图形学中z坐标也叫做深度。你可以认为这个css的坐标系的x正轴方向是从左到右，y正轴方向是从上到下，z轴方向是从屏幕里指向屏幕外的。

每个元素box都属于一个栈空间，这些元素box在栈空间内都有一个整数的**栈层级**，元素的**栈层级**可以用`z-index`，默认**栈层级**为0，同一个栈空间内，栈层级大的元素永远在栈层级小的元素的前面，栈层级大表示其z坐标大，越靠近屏幕外面，离人眼越近，所以一般我们可以通过设置`z-index`使某个元素显示在其他元素的上面。

![stacking context](https://pengfeiw.github.io/images/blog/130.jpg)

### 栈空间的创建

根元素会创建一个**根栈空间（root stacking context）**，根栈空间内的元素有可能会创建一个**局部的栈空间**，然后局部栈空间内的元素可能又会创建一个**局部栈空间内的局部栈空间**...

创建局部栈空间的元素有两个栈层级：一个是它在它所属的栈空间中的栈层级（栈层级由它的z-index设置），另一个是它在自己所创建的局部栈空间内的栈层级（栈层级为0）。

子元素的栈层级与它的父元素的栈层级相等，除非设置它的**z-index**属性为一个不同的值。

#### 1.position属性

如果设置了一个元素的position属性，那么该元素有可能会创建一个局部栈空间。具体由该元素的z-index属性确定。

`z-index`有两个作用：
1. 设置元素在所属栈空间内的栈层级。
2. 决定元素是否创建了一个局部栈空间。

`z-index`接受两种值：关键字`auto`、整数。
1. `z-index:auto;`: 元素在所属栈空间内的栈层级为0，元素不会创建新的栈空间（局部栈空间），除非该元素是页面根元素，页面根元素默认会创建一个栈空间。
2. `z-index:<interger>`: 元素在所属栈空间内的栈层级为0，设置的`<interger>`，元素会创建一个新的局部栈空间。

所以前面那个例子，我们设置了`z-index:-1;`没有效果，因为`<span>`元素处于新的局部栈空间内。而它的父元素在外层栈空间内的栈层级为0。

#### 2.其他

还有许多其他情况也可以创建新的栈空间，这里我做一个总结。
- 文档根元素（html）。
- `position`为`absolute`或`relative`的元素，并且`z-index`不为`auto`的元素。
- `position`为`fixed`或者`sticky`的元素。
- flex容器的子元素（项目），且`z-index`值不为`auto`。
- grid容器的子元素（项目），且`z-index`值不为`auto`。
- `opacity`属性值小于`1`的元素
- `mix-blend-mode`属性值不为`normal`的元素；
- 以下任意属性值不为 none 的元素：
    - `transform`
    - `filter`
    - `perspective`
    - `clip-path`
    - `mask`/`mask-image`/`mask-border`
- `isolation`属性值为`isolate`的元素。
- `-webkit-overflow-scrolling`属性值为`touch`的元素。

## 三.绘制顺序

元素的绘制顺序，影响了当两个元素重叠时，其中一个元素是否会被另一个元素遮住。

在一个栈空间内，绘制顺序从先往后大致如下。
1. 构成该栈空间元素的背景和边框（先绘制背景，再绘制边框）。
2. `z-index`为负值的并且创建了局部栈空间的元素，`z-index`最小的先绘制。
3. 处在正常文档流内，position为static的非内联（non-inline）元素。
4. position为static的浮动元素。
5. 处在正常文档流内，position为static的内联（inline）元素，包括内联table和内联块（inline blocks）。
6. `z-index`为0的并且创建了局部栈空间的元素和`z-index`为0并且position为非static的元素。
7. `z-index`为正值的并且创建了局部栈空间的元素，`z-index`最小的先绘制。

更详细的绘制顺序可以参考[这里](https://www.w3.org/TR/2012/WD-css3-positioning-20120207/#det-stacking-context)。


（完）
