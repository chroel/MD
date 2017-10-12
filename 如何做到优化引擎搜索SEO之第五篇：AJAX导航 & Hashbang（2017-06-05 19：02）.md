
前文：[《如何做到优化引擎搜索SEO（有HTML，关键字，Ajax，url，内容顺序等）》](http://blog.csdn.net/qq_2842405070/article/details/72782616)

英文原文来源：[clickhelp博客](https://clickhelp.co/clickhelp-blog/)

英文原文：[*Online Documentation and SEO. Part 5 - AJAX Navigation & Hashbang * ](https://clickhelp.co/clickhelp-blog/online-documentation-and-seo-part-5-ajax-navigation-and-hashbang/)

下文均为翻译+自己的注解和想法
<font color=darkgray>（所有ClickHelp打广告部分用浅灰色注解）</font>

------------

**<font size="4">翻译：</font>**


　　当读者浏览在线文档时，他们点击了跨媒体链接，并经常使用目录导览。有了这些用例，如果整个页面在每个导航中重新加载，这可能会损害文档的可用性。【意思就是，平常的读者是使用nav去导航到自己想看的页面，会让页面的每个导航重新加载，会损害在线文档的可用性，就像是这个↓】
　　![w3school的在线文档](http://img.blog.csdn.net/20170601120749166?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
　　

　　为了提高在线文档的响应能力，技术作者经常使用AJAX导航。这个想法很简单 - 链接点击由JavaScript处理，只有部分页面重新加载。它肯定有助于响应部分！然而，这种动态导航可能会有一些技术作者需要记住的副作用，让我们来看看它们。
　　

　　**<font size="4">导航期间的URL更改</font>**
　　

　　在最简单的实现中，浏览器的地址栏在AJAX导航期间不会改变。新内容以编程方式放置在页面上，但是在Web浏览器方面没有真正的导航。所以，如果你想链接到一个这样的在线文档的特定主题，你只需要复制当前的页面URL，它可能会指向系统的一些“主页”。


　　当动态导航发生时，一个简单的解决方案将是从JavaScript更改URL。不过，到目前为止，浏览器开始支持HTML 5时，这是不可能的。


　　为了解决不便之处，此类系统通常具有“永久链接”按钮，可为您提供可用于访问当前页面的URL。另一个解决方案是使用锚标签（page.html＃anchor1） - 可以从脚本更改锚文本而不重新加载整个页面。
　　 

**<font size="4">自己的想法：</font>**

　　首先，先解释标题，什么是Hashbang。
　　
　　下图是在知乎找到的答案↓，文章链接[在此](https://www.zhihu.com/question/19946782)
![Hashbang](http://img.blog.csdn.net/20170601093840869?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

　　看完就知道为什么这篇的标题，还要讲到Ajax导航