
**首先，为什么会提出这个问题**

在用jquery-weui开发的时候，当时还没有IOS11，所以引入FastClick完全没出现过问题，一两个月后就有客户反馈说（此时是加入fastclick的），（而且已经进入后台开发了）点击tab切换有问题（忘了这个问题描述是啥了），然后（后台问了一些细节，）花了很久才知道是IOS11的系统已经修复了点击延迟几百毫秒的问题，所以提出“ IOS11 已经解决了点击延迟的问题，引入 fastclick 反而会导致页面在 IOS 下面点击失灵；IOS 11 以下还需要引入 fastclick ，11 开始不用的问题”，然后让前端（=。=也就是我）解决一下。


**参考**

- userAgent判断 IOS 版本：https://zhidao.baidu.com/question/244020584171669444.html

- JS判断是否有js、css文件的引入方法：http://www.bcty365.com/content-69-5565-1.html


**解决**

在&lt;head>书写

	<!-- 判断ios版本 -->
	<script>
	    var str= navigator.userAgent.toLowerCase(); 
	    var ver=str.match(/cpu iphone os (.*?) like mac os/);
	    if(!ver){//非IOS系统
	        // 引入fastclick文件
	        includeFastclickJsFile();
	    }else{
	        console.log("你当前的Ios系统版本为："+ver[1].replace(/_/g,"."));
	        if(parseInt(ver[1])>=11){
	            //不必引入fastclick文件
	        }else{
	            // 引入fastclick文件
	            includeFastclickJsFile();
	        }
	    }
	
	    function includeFastclickJsFile(){
	        var oHead = document.getElementsByTagName('HEAD').item(0);  
	        let fastclick= document.createElement("script");
	        let fastclickAttach = document.createElement("script");
	        fastclick.type = "text/javascript";  
	        fastclick.src="../static/jq_weui/1.0.0/lib/fastclick.js";  
	        fastclickAttach.type = "text/javascript";  
	        fastclickAttach.src="../static/lib/fastClick/fastclick_attach.js";  
	        oHead.appendChild(fastclick);
	        oHead.appendChild(fastclickAttach);
	    }
	</script>

fastclick.js文件不用说

fastclick_attach.js文件是这样的↓

	$(function() {
	    FastClick.attach(document.body);
	});



**总结**

还从来没解决过这种问题，都忘了document.createElement("script")（虽然知道这个方法）；这样来按需引入script文件。