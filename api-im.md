# IM模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

### IM自定义消息：
| 消息type | 是否有push  | 消息说明 | 消息数据体 |
| ---- | ---- | ---- | ---- |
| picture | 是 | IM的图片消息 |``` {"medium": "fa3fdavedfa", "duration": 7)``` | 
| audio | 是 | IM的音频消息 |``` {"medium": "fa3fdavedfa", "width": 400, "height": 500)``` | 
| gift_received | 是 | 对方收到了礼物 |``` {"gift": "rose")``` | 
| system | 是 | 系统消息，目前用于用户离线后的唤醒推送 |``` {"content": "最近有美女查看了您的个人主页，快去看看吧")``` | 
| notification | 否 | im页面的通知消息 |``` {"content": "对方挑逗了你，你又可以继续勾搭美女了哦")``` | 
| discount | 是 |小助手发出的消息，用于提醒48小时或者5次未完成订单的用户有折扣商品 |``` {"content": "限时折扣VIP体验活动，超划算！真人聊骚，语音视频体验套餐低至0.8元每分钟，限时抢购，赶紧购买吧")``` | 
| video_chat | 是 | IM的视频聊天消息 |``` {"medium": "fa3fdavedfa")``` | 
| audio_chat | 是 | IM的语音聊天消息 |``` {"medium": "fa3fdavedfa")``` | 
| beauty_info  | 是 | 微信号 |``` {"title": "fa3fdavedfa",  "beauty":{"age":11, "nickname":xxx, "gender": "male", "icon":"xxxx",  "distance":10, "weixin":"xxx"}}``` | 

