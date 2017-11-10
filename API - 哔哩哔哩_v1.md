##哔哩哔哩（Bilibili）

> 本页面更新：2017.09.07
> 
> api更新：2017.10.11
 
问题/反馈：ad # imjad.cn

调用超过 716339 次

过去的 5 分钟内每分钟调用大约 1 次

###调用方法

	GET https://api.imjad.cn/bilibili/

###参数说明

get 指定请求类型，对应关系如下，默认为 playurl

get	|含义
---|---
playurl	|视频或番剧
seasoninfo	|番剧详情
source	|番剧源信息
seasonrecommend	|番剧推荐
comments	|评论
search	|搜索
rank	|排行榜
typedynamic	|分区动态
timeline	|新番时间线
recommend	|特别推荐


####视频/番剧

参数	|含义	|默认
----|-----|----
aid	|int 视频 aid，即 av 号	|无
season_id	|int番剧 season id	|无
page	|int 视频分页，为空时返回分页列表	|1
index	|int 番剧分集	|1
quality	|int 清晰度，可用值为 1~3 不等，可在分页列表查询到	|2
type	|string 视频格式，可用值为 mp4/hdmp4/flv 不等，可在分页列表查询到	|hdmp4
raw	|bool 当类型为视频或番剧时，指定是否直接 302 到视频直链	|false
action	|string 值为 update 时刷新缓存	|无


####番剧源信息

episode_id 番剧 ```episode_id```，可通过请求 seasoninfo 获取到

####番剧推荐

season_id 番剧 ```season id```


####排行榜

参数|	含义	|默认
---|---|----
type	|string 排行榜类型|	all
content	|mix 排行榜内容|	0
duration	|int 日期限制	|3
new	|bool 是否为近期投稿	|true


**排行榜类型**

type	|含义
---|---
all	|全站榜
orign	|原创榜
rookie	|新人榜
bangumi	|新番榜


**排行榜内容**

content|	含义
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

**日期限制**

duration|	含义
---|---
1	|日排行
3	|三日排行
7	|周排行
30	|月排行

*番剧和国创仅支持 3 或 7

####搜索

参数	|含义|	默认
---|---|---
keyword	|string 关键字	|无
type	|string 搜索类型	|all


**搜索类型**

type	|含义
---|---
all|	综合
bangumi|	番剧
upuser	|UP主
pgc|	影视
suggest|	结果推荐

####评论

sort 指定结果排序方式，对应关系如下，默认为 0

sort	|含义
----|----
0	|按发送时间倒序
1	|按热门排序
2	|按点赞数排序