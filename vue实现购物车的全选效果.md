**做出来的实例：**[http://h5.sz.ztbweb.cn/e-meiren/dist/mall_cart.html](http://h5.sz.ztbweb.cn/e-meiren/dist/mall_cart.html)

**实现思想：**将一组checkbox一开始的checked设置为false，就当前被电击的这个（即$(this)）被选中，就能将多选变成单选的样子

**过程：**

三、全选功能

checkbox的checked属性，如果是直接写在标签里面，无论是一下五种中的哪一种，都会被视为勾中！

- ``<input type="checkbox" checked>``
- ``<input type="checkbox" checked="">``
- ``<input type="checkbox" checked="checked">``
- ``<input type="checkbox" checked=true>``
- ``<input type="checkbox" checked=false>``.

只有removeAttribute("checked")，也就是``<input type="checkbox">``的时候才不会勾中！

![](https://hb-v4-attachment-img.huoban.com/attachment/9987337/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=biF6i9ISEiuqCq%2FQxreLdvr7ES8%3D)

如果不加上这两句话，就没办法实现全选/全不选的功能

四、js取float型小数点后两位数的方法：[http://www.jb51.net/article/45884.htm](http://www.jb51.net/article/45884.htm)

五、计算数组中的数组的总价格（用到第四点的parseFloat().toFixed(2)）

![](https://hb-v4-attachment-img.huoban.com/attachment/9991936/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=kRPI42wGs0T%2FNMxxYWo43Vn8hLg%3D)

![](https://hb-v4-attachment-img.huoban.com/attachment/9991984/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=5KjAMi3aCOUe%2Bj5G03NKqxP2Wuc%3D)

六、监听vue中的change事件：[https://segmentfault.com/q/1010000007852096/a-1020000007852693](https://segmentfault.com/q/1010000007852096/a-1020000007852693)

（因为weui里面的checkbox会选中和取消选中使用的是onChange()事件）

七、jQuery 中 attr() 和 prop() 方法的区别：[http://wenzhixin.net.cn/2013/05/24/jquery_attr_prop](http://wenzhixin.net.cn/2013/05/24/jquery_attr_prop)


八、关于全选的问题（需要参考第十三）

对于列表中每个checkbox都执行todo()，出现的bug1：勾中列表中的每一个，再取消其中一个再勾选回来，全选按钮没有被勾中

![](https://hb-v4-attachment-img.huoban.com/attachment/10079129/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=01Mgb487qzKovnhLCflzLVjq5eg%3D)

原因是：attr()  → 修改成prop()就可以了，详细见十三。

bug2：全选按钮点击之后，就算是checked=false，还是不会进入函数体内执行。

一开始如图![](https://hb-v4-attachment-img.huoban.com/attachment/10079417/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=Zy350gJOFMqdTyPFAkpo2%2FecJF8%3D)

这么写还是可以起作用的，但是修改完bug1就出现，点击全选按钮，输出它的checked状态虽然为false，但页面 的全选按钮还是显示被勾中。原因一个是逻辑问题，另外一个是attr()。但prop()改为attr()也还是不行，所以再改了一下如下图

![](https://hb-v4-attachment-img.huoban.com/attachment/10079483/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=7u9ZIh8dirDjwmeJ0imHsmd%2FOYY%3D)

发现逻辑应该是没问题了，还是进不去checked=false的判断里面，于是将$().prop("checked","false")修改成 !$().prop("checked")就没问题了。如下图

![](https://hb-v4-attachment-img.huoban.com/attachment/10079527/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=2YjJEJnk%2BZ%2BBZFCydiSIpdYL9VU%3D)

bug3：如果我在全部勾选中按钮之后，再去增加商品的数量，总价格并不会变化。

![](https://hb-v4-attachment-img.huoban.com/attachment/10079712/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=SPnVBJLMl%2FMeQKtTKwpFONeQkDQ%3D)

![](https://hb-v4-attachment-img.huoban.com/attachment/10079755/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=x12F9Usk9i9wcy%2BrQYVSbrewO80%3D)

![](https://hb-v4-attachment-img.huoban.com/attachment/10082640/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=Y4ncOp1EIEgtzRdETZ69aTm%2FNI0%3D)

修改如下：

![](https://hb-v4-attachment-img.huoban.com/attachment/10082541/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=Qh5V%2BKo7Jl7IAFDngpWUaa6lqdI%3D)

![](https://hb-v4-attachment-img.huoban.com/attachment/10082568/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=wdDI8dnInkrdf7UHrsyJZq9J%2BOw%3D)

**参考资料：**

一组checkbox从多选变单选：[http://bbs.csdn.net/topics/390597809](http://bbs.csdn.net/topics/390597809)


**效果截图：**
![](http://i.imgur.com/0HkCGhi.jpg)
![](http://i.imgur.com/gwVPDm2.jpg)
![](http://i.imgur.com/y2ptI1o.png)