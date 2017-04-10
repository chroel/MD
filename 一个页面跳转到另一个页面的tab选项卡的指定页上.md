实现目的如图
![](https://hb-v4-attachment-img.huoban.com/attachment/10009283/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3Dd058ccbf6c81800a62d595c6b63533fa838b47c1.jpg%3B%20filename%2A%3Dutf-8%27%27d058ccbf6c81800a62d595c6b63533fa838b47c1.jpg&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=wWDUFLTDJ6lYcFnwJemYMg1BuT0%3D)

1、（没去使用，据说没用）

	document.getElementById("one"+参数id).style.display="block";

2、（没去使用，据说没用）

index.html

	<a href='1.html?id=3' target='_blank'>3</a>

js

	var config;

	$('a').click(function() {

   		config = $(this).css('href').substring($(this).css('href').indexof('id=')+1)

	});

	1.html

	获得config

3、（没去使用，但是有用）

给a页面传递参数，然后a获取后显示指定的tab，显示tab内容自己看api配置

 	<a href="a.html?tab=tab3">a.html</a> 

	a.html

    var m = /tab=([^&]+)/.exec(location.search); 
    if (m) { 
        alert(m[1])//m[1]为显示的tab，自己看api进行操作 
    }


4、（有用）

a页面：

![](https://hb-v4-attachment-img.huoban.com/attachment/10011117/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=csMdHbqIKNIK2%2Fbhh0gKotb5VzA%3D)

b页面：

![](https://hb-v4-attachment-img.huoban.com/attachment/10011096/0@1000w_3000h_1l?response-content-disposition=inline%3B%20filename%3DClipboard%20Image.png%3B%20filename%2A%3Dutf-8%27%27Clipboard%2520Image.png&OSSAccessKeyId=eN8I7iifvN18lJgz&Expires=1491819600&Signature=2X8ifs%2BQ6m%2FzxTo%2BShbjp1x5Zd0%3D)