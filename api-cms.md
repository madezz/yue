# 推荐模块接口文档
[主页](Home.md)->[服务器主页](server-team.md)->[接口文档主页](api-doc.md)

cms模块的模块前缀为m_cms


## 常量定义
```python
# 帖子类型
'text'  # 文本帖子
'video'  # 视频帖子
'audio' # 音频帖子
'picture' # 图片帖子
```

## 缘分列表接口
**url**: /m_cms/lucky_list  
**method**:  GET  
**params**: 

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量 |
| limit | int | 是 | 分页大小 |
**response**:
```python
{
  "cursor": "dfaewvdaverefdafdsa2",  # 可能为空，为空并不代表没数据了。
  "total": 128,
  "items":[
  {
    "id": "fdadfa-3242fda-324fad",
    "nickname": "东方美人",
    "age": 24,
    "icon": "234dfaw345fda",   # 头像
    "video_intro": "fdafd3fdafdadf3fda"  # 这个key值不为空，说明有视频标识
    "singature":  "今晚你在哪里呢", 
    "video_price": 3,
    "audio_price":  null,   # 为null表示不同意
    "is_verified": True,  # 是否认证
 }
]
}
```

## 广场最新最热接口
**url**: /m_cms/square   
**method**:  GET    
**params**:     

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| board | string | 是 | 板块code，可选值hot, new ，是最新还是最热 |
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量 |
| limit | int | 是 | 分页大小 |
**response**:
```python
{
  "cursor": "dfaewvdaverefdafdsa2",  # 可能为空，为空并不代表没数据了。
  "items":[
  {
     "id": "23fda3fdqadfa=",  # 帖子id
     "price": 3,  # 帖子所话费的豆币数，客户端判断此字段为0时，代表此帖子免费、公开。
     "is_bought":  true,  # 当前登录用户是否购买此帖子。
     "post_type": "video", # 帖子类型，可能值video, audio, picture, text
     "content": "你们喜欢吗", # 帖子文本内容
     "media": [{           # 帖子的资源数组，视频音频帖子数组长度为1，图片帖子数组长度最多为9
              "type": "audio",  # 可能值 video, audio, picture
               "key": "dfafrt4vda3fda",
               "duration": 7,  # 只有为音频时才有这个字段
          }
     ],  
     "like_count": 80,
     "click_count": 2000,
     "is_liked": true, # 当前登录用户是否已经点赞
     "created_time": 19847290021  # 帖子发布时间， 最热列表请忽略这个字段。
     "user": {
         "id": "fdadfa-3242fda-324fad",
         "nickname": "东方美人",
         "age": 24,
         "icon": "234dfaw345fda",   # 头像
     }
 }
]
}
```

## 获取各种banner
**url**: /m_cms/banners   
**method**:  GET    
**params**:     

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| board | string | 是 | 板块code，可选值square_banner, vip_banner(vip页面的banner), coin_banner(豆币页面的banner)，city_banner(同城页面的banner)|

**response**:
```python
{
    "items": [
      {
        "url": "http://www.baidu.com",
        "img": "03b2e7de-a4b8-4029-a565-39f7e591632d"
      }
    ]
}
```

## 一键打招呼美女列表
**url**: /m_cms/greet_list  
**method**:  GET  
**params**: 
**response**:
```python
{
  "items":[
  {
    "id": "fdadfa-3242fda-324fad",
    "nickname": "东方美人",
    "age": 24,
    "icon": "234dfaw345fda",   # 头像
    "video_intro": "fdafd3fdafdadf3fda"  # 这个key值不为空，说明有视频标识
    "singature":  "今晚你在哪里呢", 
    "video_price": 3,
    "audio_price":  null,   # 为null表示不同意
    "is_verified": True,  # 是否认证
 }
]
"total":1
}
```

## 获取附近的人
**url**: /m_cms/nearby_list  
**method**:  GET  
**params**: 
**response**:
```python
{
  "items":[
  {
    "id": "fdadfa-3242fda-324fad",
    "nickname": "东方美人",
    "age": 24,
    "icon": "234dfaw345fda",   # 头像
    "video_intro": "fdafd3fdafdadf3fda"  # 这个key值不为空，说明有视频标识
    "singature":  "今晚你在哪里呢", 
    "video_price": 3,
    "audio_price":  null,   # 为null表示不同意
    "is_verified": True,  # 是否认证
    "location":"西市区.体育场南街",   #地理位置信息
    "video_chat": "fdafd3fdafdadf3fda",  # 是否认证
 }
 ]
 "total":1
}
```
