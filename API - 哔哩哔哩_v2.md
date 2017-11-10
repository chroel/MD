##哔哩哔哩_v2（Bilibili_v2）

> 本页面更新：2017.10.11
> 
> api更新：2017.11.05

问题/反馈：ad # imjad.cn

调用超过 716339 次

过去的 5 分钟内每分钟调用大约 0 次

###调用方法

	GET https://api.imjad.cn/bilibili/v2/

###参数说明

get 指定请求类型，对应关系如下，默认为 playurl

get|	含义
---|---
playurl|	视频或番剧
seasoninfo|	番剧详情
source|	番剧源信息
seasonrecommend|	番剧推荐
comments|	评论
search|	搜索
rank	|排行榜
typedynamic	|分区动态
timeline	|新番时间线
recommend	|特别推荐
space	|空间信息
archive|	投稿信息
favlist	|收藏列表

####视频/番剧

参数|	含义|	默认
---|---|---
aid	|int 视频 aid，即 av 号	|无
season_id	|int番剧 season id	|无
page	|int 视频分页，为空时返回 view 列表|	1
index	|int 番剧分集	|1
quality	|int 清晰度，可用值为 1~3 不等，可在 view 列表查询到	|2
type	|string 视频格式，可用值为 mp4/hdmp4/flv 不等，可在 view 列表查询到|	hdmp4
raw	bool |当类型为视频或番剧时，指定是否直接 302 到视频直链	|false
action|	string 值为 update 时刷新缓存	|无


####番剧源信息

episode_id 番剧 ```episode id```，可通过请求 seasoninfo 获取到

###番剧推荐

season_id 番剧 ```season id```

###排行榜

参数|	含义|	默认
---|---|---
type	|string 排行榜类型|	all
content|	mix 排行榜内容	|0
duration|	int 日期限制|	3
new	bool| 是否为近期投稿|	true

###排行榜类型

type	|含义
---|---
all		|全站榜
orign	|原创榜
rookie	|新人榜
bangumi	|新番榜

###排行榜内容

content	|含义
---|---
global	|番剧
cn	|国产动画
0	|全站
1	|动画
168	|国创相关
3	|音乐
129	|舞蹈
4	|游戏
36	|科技
160	|生活
119	|鬼畜
155	|时尚
165	|广告
5	|娱乐
23	|电影
11	|电视剧

###日期限制

duration	|含义
---|---
1	|日排行
3	|三日排行
7	|周排行
30	|月排行

*番剧和国创仅支持 3 或 7

###搜索

参数	|含义	|默认
---|---|---
keyword	|string 关键字	|无
type	|string 搜索类型	|search
page	|int 返回页数	|1
pagesize	|int 每页数量	|20
limit	|int type=hot 时返回数量	|50

###搜索类型

type	|含义
---|---
search	|搜索指定关键字
suggest	|结果推荐
hot	|热门搜索 不需要关键字

###评论

sort 指定结果排序方式，对应关系如下，默认为 0

sort	|含义
---|---
0	|按发送时间倒序
1	|按热门排序
2	|按点赞数排序

###空间信息

参数	|含义	|默认
---|---|---
vmid	|int 用户 mid	|1
pagesize	|int 作用尚不明确|	10

###投稿信息

参数	|含义	|默认
---|---|---
vmid	|int 用户 mid	|1
page	|int 返回页数	|1
pagesize	|int 每页数量	|10

###收藏列表

参数	|含义	|默认
---|---|---
fid	|int 收藏夹 fid，可在空间信息中查询到	|1
vmid	|int 用户 mid	|1
page	|int 返回页数	|1
pagesize	|int 每页数量	|20