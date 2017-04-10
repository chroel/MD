vue获取多个本地json的方法

**1、一开始：**

（参考 [ajax+jQuery实现一个页面同时加载多个模块](http://www.cnblogs.com/m-xy/archive/2013/03/06/2946013.html)）

	$.when(
		$.ajax("./static/json/weiSchool.json"), //tab1的json文件
        $.ajax("./static/json/weiSchool.json"), //tab2的json文件
        $.ajax("./static/json/weiSchool.json"), //tab3的json文件
        $.ajax("./static/json/weiSchool.json"), //tab4的json文件
        $.ajax("./static/json/weiSchool.json")) //tab5的json文件
        .then(function(a1,a2,a3,a4,a5){
            $('#tab1').html(function(){
                    for(var i=0;i<a1[0].filter_spec.goodLists.length;i++){
                        that.goodLists.push(a1[0].filter_spec.goodLists[i])
                    }
                }
            );
            $('#tab2').html(function(){
                    for(var i=0;i<a2[0].filter_spec.goodLists.length;i++){
                        that.goodLists2.push(a2[0].filter_spec.goodLists[i]) 
                    }
                }
            );
            $('#tab3').html(function(){
                    for(var i=0;i<a3[0].filter_spec.goodLists.length;i++){
                        that.goodLists3.push(a3[0].filter_spec.goodLists[i])
                    }
                }
            );
            $('#tab4').html(function(){
                    for(var i=0;i<a4[0].filter_spec.goodLists.length;i++){
                        that.goodLists4.push(a4[0].filter_spec.goodLists[i]) 
                    }
                }
            );
            $('#tab5').html(function(){
                    for(var i=0;i<a5[0].filter_spec.goodLists.length;i++){
                        that.goodLists5.push(a5[0].filter_spec.goodLists[i]) 
                    }
                }
            );
        }
    );

**2、后来看见可以直接import就好，不过json文件要放在static文件夹里面**

（参考 [Vue中如何使用fetch()获取本地.json文件](https://segmentfault.com/q/1010000007233399)）
	
    //获取data
    import data from '../../static/weiSchool.json'
    export default {
        data(){
            return {
                lists:[]
            }
        },
        mounted:function(){
            var that=this;
            that.lists=data.filter_spec.lists;
        }
    }

**3、再后来又看见使用axios的**

（参考

[Axios全攻略](https://blog.ygxdxx.com/2017/02/27/Axios-Strategy/?utm_source=tuicool&utm_medium=referral)
 
[Axios 中文说明](http://www.kancloud.cn/yunye/axios/234845)

 [github vue-axios](https://github.com/imcvampire/vue-axios) 、

[axios的用法](http://www.cnblogs.com/Upton/p/6180512.html) 、

[使用 Vuex + axios 发送请求](http://www.cnblogs.com/wisewrong/p/6402183.html) 、

[axios 并发问题](https://segmentfault.com/q/1010000007892951/a-1020000007895544)

）

	import axios from 'axios'
	axios.get(api).then((response) => {
	  	console.log(response.data)
	})
	//下面是关于同时发起多个请求时的处理
	axios.all([get1(), get2()])
	.then(axios.spread(function (res1, res2) {
		// 只有两个请求都完成才会成功，否则会被catch捕获
	}));
![axios同时发起多个请求时的处理](http://i.imgur.com/KIRCDYn.png)