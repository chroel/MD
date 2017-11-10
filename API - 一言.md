##一言（Hitokoto/ヒトコト）

> 本页面更新：2017.08.25
> api更新：2017.04.14
> 系统收录：492 个人收录：7738

问题/反馈：ad # imjad.cn

调用超过 ∞ 次

过去的 5 分钟内每分钟调用大约 ∞ 次


###调用方法

	 GET https://api.imjad.cn/hitokoto/

###参数说明

参数名 | 含义 |	默认
----|----|----
cat|string 指定source 为「0」时的分类|	任意分类
charset|string 返回字符集，支持 gbk/utf-8	|utf-8
length	|int 返回一句话的长度限制，超出则打断并添加省略号	|不限制
encode	|string 返回数据格式	|json
fun	|string 异步调用时，指定 CallBack 的函数名	|无
source	|int 值为 0 获取「系统收录」，为 1 获取「我的一言」	|随机选择

**分类说明**

参数值	|含义
----|----
a	|Anime - 动画
b	|Comic - 漫画
c	|Game - 游戏
d	|Novel - 小说
e	|原创
f	|来自网络
g	|其他


**数据格式说明**

参数值	|含义
----|----
json	|返回 JSON 格式数据
js	|返回函数名为 hitokoto 的 JavaScript 脚本，用于同步调用
jsc	|返回指定 CallBack 函数名的 JavaScript 脚本，可用于异步调用
空	|返回纯文本

