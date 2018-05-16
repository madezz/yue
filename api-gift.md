# 礼物模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

### 礼物枚举
```python
class EGift(Enum):
    """
    礼物的枚举类
    """
    LOLLY = 'lolly'  # 棒棒糖
    ROSE = 'rose'  # 玫瑰花
    MMD = 'mmd'  # 么么哒
    CUKE = 'cuke'  # 大黄瓜
    BEAR = 'bear'  # 熊宝宝
    BLUE_LOVER = 'blue_lover'  # 蓝色妖姬
    LV_BAG = 'lv_bag'  # lv包
    DIAMOND = 'diamond'  # 钻戒
    FERRARI = 'ferrari'  # 法拉利
    VILLA = 'villa'  # 别墅
```

##  获取礼物价格
**url**:  /m_gift/price   
**method**:  GET       
**params**:    无

**response**:
```python
{
    "items": [
      {
        "code": "lolly"
        "price": 1,
      }
    ]
}
```
##  赠送礼物
**url**:  /m_gift/gifts   
**method**:  POST  
**params**:   

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| to_user_id | int | 是 | 赠送的美女ID | 
| gift | string | 是 | 赠送的礼物对象 |

**response**:
```python
{}
```
**error**: 5001, 豆币余额不足

## 她的礼物列表
**url**:  /m_gift/gifts   
**method**:  GET  
**params**:   

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| user_id | int | 是 | 谁的礼物列表 | 

**response**:
```python
{
    "items": [
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
    ]
}
```
