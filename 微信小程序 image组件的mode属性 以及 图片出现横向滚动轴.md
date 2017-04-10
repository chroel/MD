本文地址：[http://blog.csdn.net/qq_2842405070/article/details/69382503](http://blog.csdn.net/qq_2842405070/article/details/69382503)

微信在3月27发布新增的六大能力中开放申请个人开发者啦！！因为公司也要做小程序，现在趁着项目在客户那边还没确定，于是自己搞了一个pixiv（也就是P站）的app（这个app名字就叫做pixiv）转成微信的小程序来练手（[github地址](https://github.com/chroel/pixiv)）。【注明：目前只是练手，至少我觉得我自己是不可能发布的，不然会被视为侵权（希望开发这个app 的 人如果看到了这个github地址觉得侵权可以联系我给撤下来）】

这次要写的是image这个组件（注意是组件不是标签）。

**写这篇文章的目的，是因为我使用image组件的mode属性中取值为缩放的时候，在图片下方出现了滚动轴。**另外就是本文章只是为了区分开mode属性中的取值问题，并不给你什么有用的或者现成的搭配。只能说，如果你也是在对mode属性存在一些疑惑的话，希望能在这篇文章受到一点提示。

按套路，先上微信官方开发文档的截图
![](http://img.blog.csdn.net/20170406103310497?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
可以看到，image这个组件有四个属性，这次针对mode属性和我所做的小程序中用到的图片结合讲一下。

按照官方的mode，分为两类：一类缩放，一类裁剪。

**我所做的pixiv是需要大量图片的网站。P站供画手们上传自己的作品。图片有大有小，按照这个，我们要做的可以分成两种**

**1.对上传上来的图片进行缩放（一般是缩小），放进我们规定好大小的格子中。**

**2.对上传上来的图片进行裁剪，假设我们只需要整张图片的中间部分就可以了。**

因为上述的这两点还要针对小程序中的view组件和scroll-view组件区分，这个涉及到了对image的width的设定，现在先讲最普通的view组件。（对于scroll-view中出现的图片， 也会出现滚动轴的情况，链接在此：[scroll-view中，image组件出现滚轴](http://blog.csdn.net/qq_2842405070/article/details/69389253)）

如图，现在我有一张这么大的图片，我只要放进这么小的格子里面。（看红框）
![](http://img.blog.csdn.net/20170406105140897?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](http://img.blog.csdn.net/20170406105437873?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

按照分类点，我们来讲第一点（缩放）我做的时候出现的问题。

这个小格子并没有规定大小，它是一个weui-flex__item，也就是flex:1（在这里就是占据了整个横面的50%）。对于image这个组件本身，我设置了width:100%（待会来看看如果把这个100% 去掉会怎样）。对于我们要调整的这张图片，首先我们明确了是缩放，也就是从scaleToFill、aspectFit、aspectFill、widthFix这四个值中取。下面就是四种对应显示的样子（看图）。
![](http://img.blog.csdn.net/20170406105840675?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](http://img.blog.csdn.net/20170406111046249?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](http://img.blog.csdn.net/20170406111050754?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](http://img.blog.csdn.net/20170406111054874?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![](http://img.blog.csdn.net/20170406111059035?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
乍一看，scaleToFill和aspectFill就是我们要用的，但是感觉好像scaleToFill和aspectFill没有区别，展示的效果都是一样一样的。这就得说回我们刚才说的，有没有给image组件设置了width:100%的问题，下面就针对有无100%来区分。

1、有设置image的width:100%

有设置100%|图片
-----------|----------
aspectFill，有设置100%|![](http://img.blog.csdn.net/20170406112333614?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
scaleToFill，有设置100%|	![](http://img.blog.csdn.net/20170406113531227?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

2、没有设置image的width:100%（可以看见，图片出现了横滚动轴）

没有设置100%|图片
-----------|----------
aspectFill，没有设置100%	|![](http://img.blog.csdn.net/20170406112843951?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
scaleToFill，没有设置100%	|![](http://img.blog.csdn.net/20170406113346053?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

一开始我做的时候，是没有给图片设置width为100%的，于是出现了滚动轴，还特别奇怪。调试一看，原来是图片原本的320px的宽度已经超出了格子的宽度，并且image组件自己已经设定好overflow:hidden（如图，没有设置width为100%的时候image的width）
![](http://img.blog.csdn.net/20170406114522501?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
对于裁剪这个，应该就不用说了吧，这个很好理解。

**结论就是：使用aspectFill或者scaleToFill最好还是给image的width设置为100%，就不会在图片下方出现横滚动轴啦。**
