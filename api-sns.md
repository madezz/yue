# 社区模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

## 获取帖子列表
**url**:  /m_sns/posts    
**method**:  GET    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| user_id | string | 否 | 按用户ID筛选 |
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量 |
| limit | int | 是 | 分页大小 |

**response**:
```python
{
  "cursor": "df3fda3fda",
  "items": [
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

## 购买帖子
**url**:  /m_sns/posts/\<post_id\>/purchases    
**method**:  POST     
**params**:  无  
**response**:    
```python
{}
```
**业务错误码**:

| 错误码 | 说明 |   
| ---- | ---- |   
| 5001 | 豆币余额不足 | 

## 发布帖子
**url**:  /m_sns/posts    
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| post_type | enum | 是 | 帖子的类型，可选值为text, video, audio, picture |
| content | string | 否 | 帖子的文本内容 |
| media | array | 否 | 帖子的图片、视频、音频等资源，把key值加密后，放在数组里传给服务器 |
| price | int | 否 | 帖子的价格，为0或为null时为公开帖子，私密的帖子把price传给服务器。 |

**response**:
```python
{}
```

## 查看帖子详情##
**url**:  /m_sns/posts/\<post_id\>    
**method**:  GET  
**params**:  

**response**:
```python
{
  "data": {
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
```
