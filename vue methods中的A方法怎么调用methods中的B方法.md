**vue.js methods中的A方法怎么调用methods中的B方法：**[https://segmentfault.com/q/1010000004939460/a-1020000004939514](https://segmentfault.com/q/1010000004939460/a-1020000004939514)
	
	var v = new Vue({ 
	  methods: { 
	    a: function() { 
	console.log('func a run !'); 
	this.b(); 
	    }, 
	    b: function() { 
	console.log('func b run !'); 
	    } 
	  } 
	}); 
	 
	v.a();

**引用到上面的知识，怎么在vue里面调用layer?**

![](https://hb-v4-attachment-img.huoban.com/attachment/10323832/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491822000&Signature=p7X%2BeGLaBRcjojPVgEaebXVAqFc%3D)

但是看到了一个感觉更好的使用vue的插件的做法（暂时还未使用过）：

github : vuejs/awesome-vue : [https://github.com/vuejs/awesome-vue#ui-layout](https://github.com/vuejs/awesome-vue#ui-layout)


**引用layer的时候，文件到底要用哪个?（推荐使用官方教程说的）**

官方：
![](https://hb-v4-attachment-img.huoban.com/attachment/10323908/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491822000&Signature=xh4jtMF9kva%2BsYVw9tlj8kI%2B%2Bgw%3D)