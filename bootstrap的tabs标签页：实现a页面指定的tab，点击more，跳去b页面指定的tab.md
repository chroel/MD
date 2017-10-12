#bootstrap的tabs标签页：实现a页面指定的tab，点击more，跳去b页面指定的tab

![实现目标](http://img.blog.csdn.net/20170516172937589?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

如图

**实现目标：** a页面的tab1标签页中点击more 跳去b页面的tab1，同理类比其他两个tab。

这里为什么是more跳过去的呢，因为tab nav上面的tab1，tab2，tab3，是用来对应自己在同个页面的标签页的。

**使用框架：** bootstrap的v3版本的tabs标签页

![bootstrap的v3版本的tabs标签页](http://img.blog.csdn.net/20170516094958269?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMjg0MjQwNTA3MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

**老生常谈：**

为当中某个标签页的```<li>```元素指定 "active"类名就可以激活当前对象

当然也可以用:first，:last，:eq(2)等的jq为指定的```<li>```元素中的```<a>```激活显示对应的标签页


 		$(function () {  
	 		$('#myTab a:first').tab('show');//初始化显示第一个tab  
	 		$('#myTab a:last').tab('show');//初始化显示最后一个tab  
	 		$('#myTab li:eq(2) a').tab('show');//选中第三个tab  
	 		$('#myTab a[href="#wanted"]').tab('show');//选中你想要的tab 
  
			$('#myTab a').click(function (e) {  
    			e.preventDefault();//阻止默认行为  
    			$(this).tab('show');//显示当前选中的链接及关联的content  
  			})  
		})  

**实现目标：** 需要跨页面实现tab的选中。（以前有做过，不过不是用bootstrap框架，等这个讲完后面补上。）

**实现思路：** a页面通过url传参（参数是tab的名称），然后在b页面进行截断获取再进行选中（通过在url传参的做法前提是不影响后台传数据）

**代码：**

	<!--a页面-->
		<ul class="nav nav-pills nav-justified" id="myTab">
   			<li role="presentation" class="active">
       			<a href="#tab1">tab1</a>
   			</li>
   			<li role="presentation">
       			<a href="#tab2">tab2</a>
   			</li>
   			<li role="presentation">
      			<a href="#tab3">tab3</a>
  			</li>
		</ul>
		<div class="tab-content">
			<div role="tabpanel" class="tab-pane active" id="tab1">
				<p>tab1 content</p>
				<a href="./detail.html?type=tab1" class="btn btn-lg">
	   				more
				</a>
		</div>
		<div role="tabpanel" class="tab-pane" id="tab2">
			<p>tab1 content</p>
			<a href="./detail.html?type=tab2" class="btn btn-lg">
			   more
			</a>
		</div>
		<div role="tabpanel" class="tab-pane" id="tab3">
			<p>tab1 content</p>
			<a href="./detail.html?type=tab3" class="btn btn-lg">
			   more
			</a>
		</div>
	</div>

	<!--b页面-->
	<ul class="nav nav-pills nav-justified" id="myTab">
	   <li role="presentation" class="active">
	       <a href="#tab1">tab1</a>
	   </li>
	   <li role="presentation">
	       <a href="#tab2">tab2</a>
	   </li>
	   <li role="presentation">
	       <a href="#tab3">tab3</a>
	   </li>
	</ul>
	<div class="tab-content">
	   <div role="tabpanel" class="tab-pane active" id="tab1">
			<p>tab1 content</p>
			<nav aria-label="...">
	           <ul class="pagination">
	                <li class="disabled">
	                    <a href="#" aria-label="Previous">
	                        <span aria-hidden="true">&lt;</span>
	                    </a>
	                </li>
	                <li>
	                    <a href="#">1 <span class="sr-only">(current)</span></a>
	                </li>
	                <li>
	                    <a href="#">2</a>
	                </li>
	                <li>
	                    <a href="#">3</a>
	                </li>
	            </ul>
	        </nav>
		</div>
		<div role="tabpanel" class="tab-pane" id="tab2">
			<p>tab2 content</p>
			<nav aria-label="...">
	           <ul class="pagination">
	                <li class="disabled">
	                    <a href="#" aria-label="Previous">
	                        <span aria-hidden="true">&lt;</span>
	                    </a>
	                </li>
	                <li>
	                    <a href="#">1 <span class="sr-only">(current)</span></a>
	                </li>
	                <li>
	                    <a href="#">2</a>
	                </li>
	                <li>
	                    <a href="#">3</a>
	                </li>
	            </ul>
	        </nav>
		</div>
		<div role="tabpanel" class="tab-pane" id="tab3">
			<p>tab3 content</p>
			<nav aria-label="...">
	           <ul class="pagination">
	                <li class="disabled">
	                    <a href="#" aria-label="Previous">
	                        <span aria-hidden="true">&lt;</span>
	                    </a>
	                </li>
	                <li>
	                    <a href="#">1 <span class="sr-only">(current)</span></a>
	                </li>
	                <li>
	                    <a href="#">2</a>
	                </li>
	                <li>
	                    <a href="#">3</a>
	                </li>
	            </ul>
	        </nav>
		</div>
	</div>
	<script>
	//标签页的点击切换
	$('#myTab a').click(function (e) {
        e.preventDefault()
        $(this).tab('show')
    })
     //判断a页面中是哪个tab标签页的more跳过来的
     var ur=location.href;
     var type=ur.split('?')[1].split("=")[1];
     switch (type){
        case 'tab1':
            $('#myTab a[href="#tab1"]').tab('show')
            break;
        case 'tab2':
            $('#myTab a[href="#tab2"]').tab('show')
            break;
        case 'tab3':
            $('#myTab a[href="#tab3"]').tab('show')
            break;
     }     
	</script>

**结论：** 看思路+代码

**感想：** 感觉除了用if，else if，else，或者是switch来区分对待它们之外，或许还有什么能节省代码量，或者提高性能，或者提高语句覆盖的方法来弄，看以后学深了就更新。

