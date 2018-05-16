# 用户模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

用户模块的模块前缀为m_user

### 几个常量定义
```python
# 对性的态度
'conservative'  # 保守
'nature'  # 顺气自然的感觉
'virgin'  # 处男/处女
'each_other'  # 两情相悦
'open'  # 开放
'crazy'  # 疯狂

# 职业
'soho'  # 自由工作者
'student'  # 在校学生
'private_owner'  # 私营业主
'white_collar'  # 白领
'institution'  # 事业单位
'agricultural'  # 农业工作者

# 学历
'junior_middle'  # 初中
'middle_school'  # 高中
'pro_training'  # 大专
'bachelor'  # 本科
'master'  # 硕士
'doctor'  # 博士

# 婚姻状况
'married'  # 已婚
'single'  # 单身
'secret'  # 保密
'in_love'  # 热恋

# 可通话时段 
'anytime'  # 随时
'work_time'  # 工作时间
'rest_time'  # 休息时间
    

```
## 登录接口
**url**：/m_user/login  
**method**: POST  
**params**: 无   
**response**:  
```python

{
  "id": "dfae23-454dfa-sfa", 
  "nickname": "阙子雄",
  "gender": "male",   #可选值为male、female
  "icon": "fda32fdaxfda23",  #加密后的key值
  "age": 24,i
  "is_vip", true, #是否会员
  "vip_left": 30, # 会员剩多少天
  "im_token": "fda3efdefda",  # im登录密钥。
}
```  
**error**：

| 错误码 | 说明 |
| ---- | --- |
| 1001 | 该用户未注册，客户端以此为依据跳转到注册 |
| 1101 | 请使用审核账号登录 |

## 审核账号登录接口
**url**：/m_user/audit_login  
**method**: POST  
**params**: 

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| account | string | 是 | 账户名 |
| password | string | 是 | 账号密码 |

**response**:  
```python

{
  "device_id": "fdaefdafdaefda",
   "user": {
        "id": "dfae23-454dfa-sfa", 
        "nickname": "阙子雄",
        "gender": "male",   #可选值为male、female
        "icon": "fda32fdaxfda23",  #加密后的key值
         "age": 24,i
         "is_vip", true, #是否会员
         "vip_left": 30, # 会员剩多少天
         "im_token": "fda3efdefda",  # im登录密钥。
   }
}
```  

## 新增用户（注册）
**url**:  /m_user/users  
**method**:  POST  
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| nickname | string | 否 | 用户昵称 |
| gender | enum | 是 | 用户性别，male, female |
| icon | string | 否 | 用户头像 |
| age | int | 是 | 用户年龄 | 

**response**:
```python
{
  "id": "dfae23-454dfa-sfa", 
  "nickname": "阙子雄",
   "gender": "male",   #可选值为male、female
   "icon": "fda32fdaxfda23",  #加密后的key值
   "age": 24,
    "is_vip", true, #是否会员
    "vip_left": 30, # 会员剩多少天
     "im_token": "fda3efdefda",  # im登录密钥。
}
```

## 修改用户
**url**: /m_user/users/\<user_id\>  
**method**: PUT/PATCH  
**paras**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| nickname | string | 是 | 用户昵称 |
| gender | enum | 是 | 用户性别，male, female |
| icon | string | 否 | 用户头像 |
| age | int | 否 | 用户的年龄 |
| signature | string | 否 | 用户签名 |
| sex_attitude | enum | 否 | 对性的态度 |
| job | enum | 否 | 职业 |
| degree | enum | 否 | 学历 |
| marriage | enum | 否 | 婚姻状况 |
| online_period | enum | 否 | 在线时间 |
| video_price | int | 否 | 视频聊天价格 |
| audio_price | int | 否 | 音频聊天价格 |



```python
 {
  "id": "dfae23-454dfa-sfa", 
  "nickname": "阙子雄",
   "gender": "male",   #可选值为male、female
   "icon": "fda32fdaxfda23",  #加密后的key值
   "sex_attitude": "open",  #对性的态度，定义为枚举值
   "age": 24
}
```
 
## 获取用户基本信息
**url**: /m_user/users/\<user_id\>    
**method**: GET   
**paras**:  无  
```python
 {
  "id": "dfae23-454dfa-sfa", 
  "nickname": "阙子雄",
  "gender": "male",   #可选值为male、female
  "icon": "fda32fdaxfda23",  #加密后的key值
  "age": 24,
  "sex_attitude": 'open',
  "job": "student",
  "degree": "doctor",
  "marriage": "secret",
  "signature": "哈哈",
  "video_price": 0,
  "audio_price": 3,
  "online_period": "anytime",

    # 以下信息只在用户是登录用户时返回
   "is_vip": true,
    "vip_left": 30, # 会员剩多少天
}
```
 
## 用户的个人中心
**url**: /m_user/users/\<user_id\>/homepage   
**method**: GET   
**paras**:  无    
```python
 {
  "id": "dfae23-454dfa-sfa", 
  "nickname": "阙子雄",
  "gender": "male",   #可选值为male、female
  "icon": "fda32fdaxfda23",  #加密后的key值
  "age": 24,
  "signature": "我的青春小鸟飞走了",
  "background": {
    "type": "video", # 背景类型，一般为视频，没有视频时会返回type为picture
    "key": "fda23rdfaf3fda",  # 资源key值
  },
  "audio_intro": {  # 音频介绍
     "type": "audio",
     "key": "fda23wfdar3fda",
     "duration": 7,
   },   
  "job": "student",  # 工作， 以下几个枚举值，查看文档最前的常量
  "degree": "master",  # 教育水平
  "marriage": "in_love", # 婚姻状况
  "sex_attitude": "open", # 对性的态度
  "video_price": 1,
  "audio_price": 3,
  "is_vip": true, # 是否是vip
  "online_period": "anytime",  # 可通话时段，见常量
  "profit": 5300, # 累计赚取
  "her_gifts": [
      "from_user": {
         "id": 'dfa3fd3fe',
         "icon": 'fda3fdef3fa',
      }
      "gifts": [
        {
            "code": "villa",
            "count": 5,
        }
      ]
    ],
  "post_count": 20, # 动态数量
  "posts": [  # 前五条视频、图片动态，所以即使post_count为5，这里也可能少于5
    {
      "id": "dfa34fda3fda",
      "post_type": "picture",
      "media": [{           
              "type": "audio",  # 可能值 video,  picture
               "key": "dfafrt4vda3fda",
          }
     ],  
    }
  ]
}

```

## 点赞与取消点赞
**url**: /m_user/likes    
**method**:  POST/DELETE  
**paras**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| target_id | string | 是 | 点赞的目标id，如帖子id |
| target_type | string | 是 | 点赞的目标类型，目前只能为"post" |

```python
{}
```

## 新增用户反馈
**url**: /m_user/feedbacks    
**method**:  POST  
**paras**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| content | string | 是 | 反馈的内容 |

```python
{}
```

## 统计用户信息
**url**: /m_user/user_tracks    
**method**:  POST  
**paras**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| push_status | Boolean | 否 | 用户的消息推送开关是否打开 |
| lng | float | 否 | 经度，获取不到传空 | 
| lat | float | 否 | 纬度，获取不到传空 |

```python
{}
```

## 单独获取im登录接口
**url**: /m_user/im_token    
**method**:  GET  
**paras**:    无

```python
{
  "im_token": "fda3fvdafedafad"
}
```

## 获取帖子评论列表
**url**:  /m_user/comments  
**method**:  GET    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| target_id | int | 是 | 实体id |  
| target_type | string | 是 | 实体类型('post':动态) |  
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量 |
| limit | int | 是 | 分页大小 |  

**response**:
```python
{
  "cursor": "df3fda3fda",
  "total": 128,
  "items": [
    {
     "id": "23fda3fdqadfa=",  # 评论id
     "content": "你们喜欢吗", # 评论文本内容
     "created_time": 19847290021  # 评论发布时间
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

## 发布帖子评论
**url**: /m_user/comments  
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| target_id | int | 是 | 实体id |
| target_type | string | 是 | 实体类型('post':动态) |  
| content | string | 是 | 帖子的内容 |  

**response**:
```python
{}
```

## 获取用户语音、视频聊天资源
**url**: /m_user/user_chat_media  
**method**:  GET  
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- | 
| chat_type | string | 是 | 'video_chat' or 'audio_chat' |  
| user_id | string | 是 | 用户id |  

**response**:
```python
 {
        "key": "bbfa9ff8-5d95-445b-93b1-12e598cec7bd",
        "type": "video"
 }
```
