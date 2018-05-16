# 用户行为数据接口
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

> 本页面的接口使用HOST,  http://meiyuxiuxiu.f3322.net:19567

## 获取用户行为数据

**url**: /behaviors  
**method**: GET  
**params**:    

|  参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| user_id | int | 是 |  要筛选的用户ID |
| ct_start | datatime | 是 | 创建时间开始 |
| ct_end | datatime | 是 | 创建时间结束 |
| offset | int | 是 | 分页参数 |
| limit | int | 是 | 分页参数 |
**response**:
```python
{
  "total": 1223,
  "items": [
       {
        "eid": "click_post",
        "created_time": 1323000, # 事件发生时间
         "version": "Android/1.1", # 用户所在的版本号
         "ext":  {}  # 行为的其他参数，根据事件id不同而不同
         "action": "回复了美女32：你好啊美女",   # 行为的具体内容描述。
   }
 ]
}
```
