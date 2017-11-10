##二维码（QR Code）

> 本页面更新：2017.06.23

> api更新：2017.09.03

问题/反馈：ad # imjad.cn

调用超过 520934 次

过去的 5 分钟内每分钟调用大约 3 次


###调用方法

	GET https://api.imjad.cn/qrcode/

###参数说明

参数名|	含义|	默认
----|----|----
text	|string 待转换内容，最大 512Byte，请使用 utf-8 字符集并进行 urlencode	|https://api.imjad.cn/qrcode.md
logo	|string 二维码中间 logo 的地址，最大 200KiB	|无
size	|int 二维码大小，单位 px，最大 500	|200
level	|string 冗余度，可用值为 L/M/Q/H	|M
bgcolor |string 背景色，应为十六进制	|#FFFFFF
fgcolor	|string 前景色，应为十六进制	|#000000
encode	|string 返回数据格式	|raw
fun	|string 用于异步调用时，指定 CallBack 的函数名	|qrcode

**返回数据格式说明**

encode	|含义
---|---
raw	|返回 MIME 类型为 image/png 的图像数据
json	|返回 JSON 格式数据
js	|返回函数名为 qrcode 的 JavaScript 脚本，用于同步调用
jsc	|返回指定 CallBack 函数名的 JavaScript 脚本，可用于异步调用

备注：服务器缓存保留 7 天