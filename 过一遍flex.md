这篇来讲 
**display:flex**

----

**主要内容参考来自**

1. [布局模式](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Layout_mode)

2. [外边距合并](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)

1. [Flex 布局教程：语法篇 —— 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

1. [Flex 布局教程：实例篇 —— 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

1. [css-align-items —— MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)

---

**目录顺序**

- 布局模式
- 盒模型
- display
	- Flexible Box / Flexbox
		- 定义
		- 来源
		- 概念
		- 容器的属性
		- 项目的属性
		- 易理解错的示例
	- flexbox和box有什么区别

----

## 布局模式

**css布局模式**，简称布局，是一种算法，基于盒子与其兄弟、祖辈盒子的交互方式来确定盒子的位置和大小

分下面几种

 - 块布局
 - 行内布局：例如文本
 - 表格布局：表格
 - 定位布局：position
 - 弹性盒子布局：Flexible Box 或 Flexbox (需兼容)
 - 网格布局：display:grid;


**盒模型**

![盒模型](https://mdn.mozillademos.org/files/8685/boxmodel-(3).png)

涉及到的属性有

- width
- min-width
- max-width
- height
- min-height
- max-height
- margin（不展开）
- padding（不展开）
- border（不展开）
- overflow
- overflow-x
- overflow-y
- visibility
- box-sizing

   
<font color="#aaa">=======华丽丽的分割线=======</font>

width原理是，width如果是有padding以及border就会包括padding和border，没有的话就是只有content的宽度；height同理。

width涉及到min和max。height的min和max同理。

min-width 属性为给定元素设置最小宽度。它可以阻止 width 属性的应用值小于 min-width 的值。
min-width 的值会同时覆盖 max-width 和 width。
![min-width取值](https://i.imgur.com/vqFelob.png)

max-width 属性用来给元素设置最大宽度值。定义了max-width的元素会在达到max-width值之后避免进一步按照width属性设置变大。
max-width 会覆盖width设置, 但 min-width设置会覆盖 max-width.
![](https://i.imgur.com/ub4ELyA.png)

<font color="#aaa">=======华丽丽的分割线=======</font>

margin会涉及到一个比较特殊的情况叫做外边距合并，或者叫外边距塌陷
（margin collapsing）；

发生外边距塌陷的三种基本情况:

1. 相邻的兄弟姐妹元素
2. 块级父元素与其第一个/最后一个子元素
3. 空块元素
4. 正负间距之间的抵消


![相邻的兄弟姐妹元素](https://i.imgur.com/ez6946q.png)
![块级父元素与其第一个/最后一个子元素](https://i.imgur.com/8GL5sYi.png)
![空块元素](https://i.imgur.com/LG9EdlA.png)
![正负间距之间的抵消](https://i.imgur.com/y7kdK34.png)

<font color="#aaa">=======华丽丽的分割线=======</font>

box-sizing：**一些专家甚至<font color="red">建议所有的Web开发者们将所有的元素的box-sizing都设为border-box。</font>**
![](https://i.imgur.com/oXMPksu.png)

值类型 | 值 | 含义
----|----|-----
关键字值 | content-box | 默认值，就是width = 内容的宽度，height = 内容的高度。宽度和高度都不包含内容的边框（border）和内边距（padding）。
|border-box|包括border和padding，就是width = border + padding + 内容的  width；height = border + padding + 内容的 height。
全局值|inherit|
|initial|
|unset|




---------

##display

display CSS属性指定用于元素的呈现框的类型，生成多种不同的生成的元素的盒类型

![display取值](https://i.imgur.com/25Eqe8D.png)


---

### Flexible Box / Flexbox
	
####（一）定义

什么是flex：Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
	<div class="container">
		<div class="item"></div>
		<div class="item"></div>
		<div class="item"></div>
	</div>

	<style>
		.container{
			display:flex;
			flex:num;
			align-items:value;
		}
	</style>

	
#### （二）来源

为什么会有flex这个取值：摘自[《Flex 布局教程：语法篇 —— 阮一峰的网络日志》](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

	“布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。”

	“2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。”

这个属性的使用值得注意的地方在于

- 任何一个容器都可以指定为 Flex 布局。

	.box{
	  display: flex;
	}

- 行内元素也可以使用 Flex 布局。

	.box{
	  display: inline-flex;
	}

- Webkit 内核的浏览器，必须加上-webkit前缀。

	.box{
	  display: -webkit-flex; /* Safari */
	  display: flex;
	}

- <font color="#ff0000">设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。</font>


#### （三）概念

![flex的基本概念](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

有这么几个概念

1. 采用flex布局的元素，称为flex容器（flex container）
2. 该容器的所有子元素自动称为容器成员，称为flex项目（flex item）
3. 容器默认存在两根轴，水平的主轴（main axis）和垂直的交叉轴（cross axis）
4. 主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end
5. 交叉轴的开始位置叫做cross start，结束为止叫做cross end
6. 项目默认沿主轴排列
7. 单个项目占据的主轴空间较main size
8. 单个项目占据的交叉轴控件叫做cross size

####（四）容器的属性

容器有6个属性

1. flex-direction
2. flex-wrap
3. flex-flow
4. justify-content
5. align-items
6. align-content

<font color="#aaa">=======华丽丽的分割线=======</font>

1.0 flex-direction属性决定主轴(main)的方向（即项目的排列方向）

	.box {
	  flex-direction: row | row-reverse | column | column-reverse;
	}


值 | 含义
----|----
row（默认值）|主轴为水平方向，起点在左端。
row-reverse | 主轴为水平方向，起点在右端。
column | 主轴为垂直方向，起点在上沿。
column-reverse | 主轴为垂直方向，起点在下沿。


![flex-direction的取值对应的图](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)


<font color="#aaa">=======华丽丽的分割线=======</font>

2.0 flex-wrap属性，定义如果一条轴线拍不下，如何换行

	.box{
	  flex-wrap: nowrap | wrap | wrap-reverse;
	}


![flex-wrap取值](https://i.imgur.com/Hp6QOB9.png)

<font color="#aaa">=======华丽丽的分割线=======</font>

3.0 flex-flow属性，为flex-direction属性和flex-wrap属性的简写形式，默认值row nowrap

	.box {
	  flex-flow: <flex-direction> || <flex-wrap>;
	}


<font color="#aaa">=======华丽丽的分割线=======</font>

4.0 justify-content属性定义了项目在主轴(main)上的对齐方式

	.box {
	  justify-content: flex-start | flex-end | center | space-between | space-around;
	}

![justify-content取值](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

这里的flex-start就是main start、flex-end就是main end的位置

值 | 含义
----- | -----
flex-start | 默认值，左对齐，就是main start的位置
flex-end | 右对齐，就是main end的位置
center | 居中，main cross的中间
space-between | 两端对齐，项目之间的间隔都相等
space-around | 每个项目两侧的间隔相等。项目之间的间隔比项目与边框的间隔大一倍


<font color="#aaa">=======华丽丽的分割线=======</font>

5.0 align-items属性定义项目（items）在交叉轴（cross）上如何对齐

	.box {
	  align-items: flex-start | flex-end | center | baseline | stretch;
	}

![align-items取值](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

值 | 含义
---- | ----
flex-start | 交叉轴（cross）的起点对齐，就是cross start的位置
flex-end | 交叉轴的终点对齐，就是cross end的位置
center | 交叉轴的中点对齐
baseline | 项目（item）的第一行文字的基线对齐
stretch | 默认值，如果项目未设置高度或设置为auto，将占满整个容器的高度


<font color="#aaa">=======华丽丽的分割线=======</font>

6.0 align-content属性，定义了多根轴线的对齐方式、如果项目只有一根轴线，该属性不起作用

	.box {
	  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
	}

![align-content的取值](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)

值 | 含义
----- | -----
flex-start | cross start
flex-end | cross end
center | corss center
stretch | 默认值，轴线占满整个交叉轴。有n个轴线则每个轴线的高度为容器高度的n/100%高度
space-between | 与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around | 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。


#### （五）项目的属性

项目的属性有6个

1. order
2. flex-grow
3. flex-shrink
4. flex-basis
5. flex
6. align-self

<font color="#aaa">=======华丽丽的分割线=======</font>

1.0 order属性，定义项目的排列顺序，数值越小，排列越靠前，默认为0

	.item {
	  order: <integer>;
	}

![order属性](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

<font color="#aaa">=======华丽丽的分割线=======</font>

2.0 flex-grow属性，定义项目的方法比例，默认为0，即如果存在剩余空间也不放大

	.item {
	  flex-grow: <number>; /* default 0 */
	}

![flex-grow属性](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

<font color="#aaa">=======华丽丽的分割线=======</font>

3.0 flex-shrink属性，定义了项目的缩小比例，默认为1，如果取值0，就代表不缩小。负值对该属性无效

	.item {
	  flex-shrink: <number>; /* default 1 */
	}

![flex-shrink属性](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

<font color="#aaa">=======华丽丽的分割线=======</font>

4.0 flex-basis属性，定义了在分配多余空间之前，项目占据的主轴空间（main size）。
默认值为auto，即项目的本来大小。

	.item {
	  flex-basis: <length> | auto; /* default auto */
	}

它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

<font color="#aaa">=======华丽丽的分割线=======</font>

5.0 flex属性，是flex-grow，flex-shrink和flex-basis的简写，默认值为0 1 auto;后两个属性可选。

	.item {
	  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
	}

该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

<font color="red">**建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。**</font>

<font color="#aaa">=======华丽丽的分割线=======</font>

6.0 align-self属性，允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认auto，表示继承父元素的align-items属性。如果没有父元素，则等同于stretch

	.item {
	  align-self: auto | flex-start | flex-end | center | baseline | stretch;
	}

![align-self取值](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)


####（六）易被误导的示例

flex-grow

![](https://i.imgur.com/BrCWW5T.png)

那既然会因为文字的宽度去修改到它的宽度，要怎么解决呢？
看上文有一个重点是，不要拆开写那三个属性，并且后面两个元素使用默认值

![](https://i.imgur.com/bjo3qZC.png)


#### （七）例子

[《Flex 布局教程：实例篇》](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

----------------

### Flexbox和box的区别

今年都2017了，支持不支持什么的应该都没啥了

大概就是

1. box的话，文字超出是不会撑开div的吧；但是flex就会，像这样

![Flexbox和box](https://i.imgur.com/DSNMPbv.png)

2. box的布局不影响float等，但是flex会

![flex会影响float](https://i.imgur.com/bAZsmDg.jpg)

