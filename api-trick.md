# 套路与话术模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

## 获取套路配置
> 客户端每次被唤起时，更新此配置

**url**:  /m_trick/config      
**method**:  GET    
**params**:  无

**response**:
```python
{
  "non_vip_max_hello": 10,  # 非vip一天最多的招呼数量
  "homepage_remain_time": 60,  # 在个人主页和动态停留超过60s，触发一条话术
  "post_like_count": 2,  # 对个人动态点2个赞促发被关心话术
  "msg_polling_period": 30,  # 每隔30s进行一次polling拉取数据，设置默认值为30
  "ping_interval": 30,  # 客户端ping的时间间隔，如果没取到，默认30s
  "max_replies": 2,  # IM会话的最多回复条数
}
```


## 男性主动打招呼话术触发
**url**:  /m_trick/hello_tricks      
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| lng | float | 否 | 经度，获取不到传空 | 
| lat | float | 否 | 纬度，获取不到传空 |
| to_user_id | string | 是 | 被打招呼的美女机器人 |


**response**:
```python
{
      "msg_type": "text",  # 目前只可能为text
      "medium": "美女你好啊？",  # 文本内容或者图片等资源
      "created_time":  1322342300,  # 消息的发送时间
      "to" :  "dfafvefda=",  # 对哪个女性用户id
      "to_nickname": "小野猫", 
      "to_icon": "faevdafefda",
}
```

> 客户端保证用户只会对同一个美女打一次招呼；      
如果此接口服务器返回为空，说明此类型的消息套路已经被用户，客户端提醒用户成为会员。（会员用户，服务器允许传回重复的套路）   

## 美女被关心、随机话术、视频语音话术触发
**url**:  /m_trick/tricks      
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| trick_type | Enum | 是 | 可选值为：be_noted(美女被关心后触发), random_hello(随机触发招呼), video_audio(触发语音视频话术)| 
| lng | float | 否 | 经度，获取不到传空 | 
| lat | float | 否 | 纬度，获取不到传空 |
| to_user_id | string | 否 | 被关心的美女机器人，trick_type为be_noted时必须传 |


**response**:
```python
{}
```
> 客户端注意事项： video_audio类型的话术，每天只触发一次

## 客户端轮询拉取消息
**url**:  /m_trick/tricks      
**method**:  GET    
**params**:  

**response**:
```python
{
  items: [
    {
      "msg_type": "text",  # 目前可能为text, picture, audio,   rt_video(realtime video), rt_audio
      "content": {
           "type": "picture",   # 可为text, picutre, audio
           "medium": "dfefezdf3er3edfa",  # key值或者文本内容
           "duration": 4,  # 音频长度，type非audio没有此字段
           "width":  288,  # 图片宽度，像素, type非picture没有此字段
           "height": 444, # 图片高度, type非picture没有此字段
       }
      "created_time":  1322342300,  # 消息的发送时间
      "from" :  "2343fda3=",  # 来自于谁id
      "from_nickname": "北方的狼", # 来自于谁，昵称
      "from_icon": "fda3fda3fda", # 来自于谁，头像，    别怪id,头像，icon这三个字段没有封装在一起，ios和android不统一。
    }
  ]
}
```

## 用户回复
**url**:  /m_trick/replies   
**method**:  POST       
**params**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| to_user_id | int | 是 | 回复的用户 | 
| msg_type | string | 是 | 消息类型，可选值为, text, picture, audio,rt_video(实时视频), rt_audio(实时语音) |
| content | string | 否 | 回复的内容，如果是音频、图片，这里是加密后的七牛key | 

**response**:
```python
{}
```

##  谁看过我列表
**url**:  /m_trick/visitors     
**method**:  GET         
**params**:      

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量  |
| limit | int | 是 | 分页大小 |
| is_detail | bool | 否 | 是否获取详细的信息，服务器据此，清楚小红点 |

**response**:
```python
{
  "cursor": "df3fda3fda",
  "total": 14,  # 14个人看了你
  "has_red_dot": true, # 是否应该显示小红点
  "items": [
   { 
     "id": "23fda3fdqadfa=",  # 用户id
     "icon": "fda34fda3fda", # 用户头像
     "nickname":  "我是妹妹",  # 用户昵称
     "signature": "每天都在线哦"
   }
  ]
}
```

##  ping接口
> 客户端每次页面被切换到前台时，调用一次此接口。之后每隔一个时间段"ping_interval“决定，调用一次此接口；   
>  页面被切换到后台之后，不再调用此接口

**url**:  /m_trick/ping      
**method**:  POST         
**params**:    无

**response**:
```python
{}
```

##  发起挑逗
**url**:  /m_trick/teases       
**method**:  POST         
**params**:      

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| to_user_id | string | 是 | 被挑逗的对象id |

**response**:
```python
{}
```
**error**: 5001, 豆币余额不足

##  跑马灯提醒
**url**:  /m_trick/tips       
**method**:  GET         
**params**:      

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| tip_type | enum | 是 | 可选值，'global'(首页的提醒), 'pay_page'(充值页面的提醒) |
| cursor | string | 是 | 分页游标 |
| offset | int | 是 | 分页偏移量  |
| limit | int | 是 | 分页大小 |

**response**:
```python
{
  "cursor": 3,
  "items": [
   "恭喜“猎人”开通黄金会员成功！",
   "恭喜“z 先生”购买138豆币成功！",
   "樱桃”提现326元成功！"
]
}
```
