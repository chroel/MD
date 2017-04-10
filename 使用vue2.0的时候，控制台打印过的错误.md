vue 2.0的错误提示：

**1. component lists rendered with v-for should have explicit keys.**

看此链接：[https://segmentfault.com/q/1010000008673359](https://segmentfault.com/q/1010000008673359)

参考[官方 release note](https://github.com/vuejs/vue/releases/tag/v2.2.0)

**2.使用 vue.js 的 get/post请求错误 “ Cannot read property 'get' of undefined”**

	this.$http.get("data/address.json",{}).then(function (response) {
	});

找到：因为控制台打印出来的this，里面根本没有$http
![控制台打印出来的this](http://i.imgur.com/auWdpOU.png)