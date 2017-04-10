上一篇文章讲到[在普通的view中，使用image出现了横向的滚轴](http://blog.csdn.net/qq_2842405070/article/details/69382503)
              
这次讲到是在scroll-view中的image，暂时不写scroll-view了，我自己也对它了解甚少，有其他博主肯定写得比我这个新手好。

这篇地址：[http://blog.csdn.net/qq_2842405070/article/details/69389253](http://blog.csdn.net/qq_2842405070/article/details/69389253)

这次出现在我写的pixiv的小程序（依旧附上github地址：[github-pixiv](https://github.com/chroel/pixiv)）中的问题是，图片出现了滚动轴，而且横轴纵轴都有。如图：
         
![图片](http://img.blog.csdn.net/20170406140528733?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
                
和在[《微信小程序 image组件的mode属性 以及 图片出现横向滚动轴》](http://blog.csdn.net/qq_2842405070/article/details/69382503)中图片出现滚动轴的原因一样，都是因为设置了固定的图片的大小，以至于图片真正的大小是这样的：
            
![图片](http://img.blog.csdn.net/20170406141539622?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
          
所以（自以为是的┑(￣Д ￣)┍）就去给图片设置了width:100%
       
![这里写图片描述](http://img.blog.csdn.net/20170406141726953?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
          
发觉高度也不对，还存在着纵滚动轴，于是去设置height:100%
                   
![这里写图片描述](http://img.blog.csdn.net/20170406142033126?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)       
             
但是还是存在着纵向的滚动轴。这我就一脸懵逼了。。[黑人问号？？？]
                   
尽管没能明白具体原因，但是被我<span style="text-decoration:line-through">（假的多年开发经验）</span>一试 ，问题在image设置的display:inline-block; 被我改成display:block倒也起作用了。
（正好对比一下在前面提到的mode取值中mode="aspectToFill"和mode="aspectFill"的区别能在这里很好地体现出来图片的问题）

 mode取值      | 图片           
 ------------- |-------------
 mode="aspectToFill"（就是图片被压缩得挺难看的）     | ![图片](http://img.blog.csdn.net/20170406142849318?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 
 mode="aspectFill"（这个的图片就好看很多）    | ![这里写图片描述](http://img.blog.csdn.net/20170406143553680?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)     
				                  
至于为什么image的display属性是一开始就被为inline-block呢，找到inline-block的解释是（链接：[block，inline和inline-block概念和区别](http://www.cnblogs.com/KeithWang/p/3139517.html)）
> display:inline-block
简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。

也就是说，inline-block只是为了让image拥有block的宽高，又能和inline一样并排同行。img标签在css中的设定是block元素，image组件在微信小程序的设定是inline-block元素。

至于为什么image被我改成了display为block之后还是能并排呢？是因为包裹着这个image组件的父组件view的class就设定了这个父组件是display:inline-block，所以还能一排展现。（如图，父元素是display:inline-block）
![图片](http://img.blog.csdn.net/20170406150128241?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

--------------
| 然后问题来啦！！        | 然后又是试试试          
| ------------- |:-------------:
| 1、如果设置image的display为inline会怎样？（仍然保留width:100%和height:100%）     | 1、对于设置image的display为inline（仍然保留width:100%和height:100%），不会怎么样，和设置display为block（仍然保留width:100%和height:100%）表现一样。<br/>inline对宽度的定义是，其宽度随元素的内容而变化。 
| 2、设置image的display为block，去掉width:100%和height:100%会怎样      | 2、设置为block的image，没有了width:100%和height:100%，而是用320和240，就会出现滚轴（而且无论是横轴还是纵轴都出现！！~~搞事情太激动！！~~）     
| 3、设置image的display为inline，去掉width:100%和height:100%会怎样 | 3、不会怎么样，因为本身image的宽高就是320和240      
                    
~~搞事情的来啦~~
针对表格的第2点，明明设置的是block，按照css的定义，默认情况下，block元素宽度自动填满其父元素宽度，却又出现了滚轴（如下图）
![这里写图片描述](http://img.blog.csdn.net/20170406152316361?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

于是没办法。。
		
**结论就是：**

**1、在scroll-view中，image的缩放取值 aspectFill 比 aspectToFill 好**

**2、在scroll-view中，image的display为inline-block会导致图片出现横纵轴的滚动条，解决方案有两种（前提包裹着这个image的父组件也必须是inline-block才会滚动）**
     
 - **image的display为inline**
 - **image的display为block，同时设置image的width:100%;height:100%;**  