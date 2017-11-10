##网易云音乐（Cloudmusic）

> 本页面更新：2017.08.25
> 
> api更新：2017.10.11

问题/反馈：ad # imjad.cn

调用超过 2893500 次

过去的 5 分钟内每分钟调用大约 5 次


###调用方法

	 GET https://api.imjad.cn/cloudmusic/

###参数说明

参数名 | 含义 |	默认
----|----|----
type|string 指定请求类型|	song
id|	int 分类对应的ID	|必需

###类型相关

type	|含义
----|----
song	|单曲
lyric	|歌词
comments	|评论
detail	|歌曲详情
artist	|歌手
album	|专辑
playlist	|歌单
mv	|MV
djradio	|主播电台
dj	|主播电台单曲 id
detail_dj	|主播电台歌曲详情
search	|搜索


**单曲**

参数名|	含义|	默认
----|----|----
br	|int 指定歌曲码率，可用值为 64000,128000,198000,320000	|128000
raw	|bool 指定是否直接 302 到歌曲直链，可用值为 true 或 false	|false


**搜索、歌手、评论**

参数名|	含义|	默认
----|----|----
limit	|int 指定返回结果数量	|20
offset	|int 指定偏移数量，用于分页	|0


**搜索相关**

参数名|	含义|	默认
----|----|----
s	|string 关键词|	无
search_type	|int 搜索类型|	1


**搜索类型**

search_type|	含义
----|----
1	|单曲
10	|专辑
100	|歌手
1000	|歌单
1002	|用户
1004	|mv
1006	|歌词
1009	|主播电台