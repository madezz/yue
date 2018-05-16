# 数据统计模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

## 新增统计事件
> 统计事件接口的设计保持和友盟接口一致    
以Android为例，对应了`MobclickAgent.onEvent(Context context, String eventId, HashMap map)`接口   
和`MobclickAgent.onEventValue(Context context, String id, Map<String,String> m, int du)`接口
  
**url**:  /m_statistic/events        
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| event_id | string | 是 | 事件id，和友盟的自定义定义保持一致 |
| event | json | 否 | 事件的参数，以key-value的形式组成json字符串  |
| du | int | 否 | 计算事件的数值字段，和友盟接口保持一致 |

**调用举例**：   
计数事件，以点击个人主页(click_homepage)为例，传给服务器的参数如下:   
```python
{
  "event_id": "click_homepage",
  "event":  {  # 事件参数
       "post_id": "12"
   },
}
```
计算事件，以购买豆币(buy_coin)为例，传给服务器的参数如下：
```python
{
  "event_id": "buy_coin",
  "event": {}  # 两种事件这个字段都不是必需，但根据事件的定义都可以拥有此字段。
  "du":  6900,  # 价格为69的豆币
}
```

**response**:
```python
{}
```
