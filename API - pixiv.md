##Pixiv

> 本页面更新：2017.10.19
>
> api更新：2017.11.04

问题/反馈：ad # imjad.cn

调用超过 2006733 次

过去的 5 分钟内每分钟调用大约 15 次

###调用方法

	GET https://api.imjad.cn/pixiv/v1/

###参数说明

参数|	含义|	默认
---|---|---
type|	string 指定类型|	illust
id|	int 分类对应的ID	|无
action|	string 值为 update 时刷新缓存|	无

###类型

type	|含义
---|---
illust	|作品详情
member	|用户详情
member_illust|	用户作品
favorite	|用户收藏
rank	|排行榜
search	|搜索
latest	|最新作品
tags	|热门标签


###排行榜

参数值	|含义	|默认
---|---|---
content	|string 排行榜内容	|all
mode	|string 排行榜类型	|weekly
page	|int 指定返回页数	|1
per_page	|int 指定每页返回数量	|20

**排行榜内容**

content|	含义
---|---
all	|综合
illust|	插画
manga	|漫画
ugoira	|动图


**排行榜类型**

mode|	含义
---|---
daily|	日榜
weekly|	周榜
monthly|	月榜
rookie|	新人
original|	原创
male	|男性向
female|	女性向
...|	and more

###搜索

参数值	|含义|	默认
---|---|---
word	|string 关键字|	无
mode	|string 搜索类型	|tag
order	|string 排序方式	|desc
period	|string 排序周期，仅当 order=asc 时生效	|all
page	|int 指定返回页数	|1
per_page	|int 指定每页返回数量	|30

**搜索类型**

mode	|含义
---|---
text	|标题/描述
caption	|描述
tag	|非精确标签
exact_tag	|精确标签


###排序方式

order|	含义
---|---
desc	|按日期倒序
asc	|按日期正序


**排序周期**

period	|含义
---|---
all|	所有
day	|一天之内
week	|一周之内
month	|一月之内

备注：
illust/member/rank content=all 的前 50 条 将被缓存
返回时区为 UTC+9