# 控制台：支付模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

## 查询订单接口

**url**:  /m_pay/ pay_orders   
**method**: GET    
**params**:    

|  参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| channel  | enum | 否 | 支付渠道，可选值为wx(微信), ali(支付宝), apple(苹果支付) |
| status | enum | 否 | 支付状态，可选值为unpaid, paid |
| ct_start | datetime | 否 | created_time_start 创建时间开始值 |
| ct_end | datetime | 否 | created_time_end 创建时间结束值 |
| offset | int | 否 | 分页参数 |
| limit | int | 否 | 分页参数 |

**response**:
```python
{
   "total": 29,
   "pay_orders": [
        {
            "order_no": "234234fd343",  # 订单号
            "amount" : 12300,  # 订单金额， 分
             "subject":  "豆币69个", # 订单描述、标题
              "status": "unpaid", # 订单支付状态
             "channel": "wx",  # 订单支付渠道
              "user_id":  12,  # 用户的id
               "channel_code":  "oppo",  # 用户的渠道
              "created_time":  133235400,  # 订单创建时间
        }
   ]
}
```
