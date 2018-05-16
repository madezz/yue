# 商城模块
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

商城模块的模块前缀为m_mall， **商城模块是与RMB相关的内容**，与豆币购买相关的，出门左转[豆币模块](api-coin)

## 豆币商品列表
**url**:  /m_mall/product/coins  
**method**:  GET    
**params**:  不分页，无参数   
**response**:  
```python
{
   valid_channels: ['apple'],  # IOS客户端判断数组第一个值是否是apple来决定使用苹果支付还是支付宝和微信。
    items: [
        {
         "id": 3,
         "amount": 129,  # 豆币个数
         "price": 12900,  # 按分计算，注意，所有与RMB相关的单位，都是按分传递
         "desc": "+返100话费",
        }
    ]
}
```

## VIP商品列表v1
**url**:  /m_mall/product/vips  
**method**:  GET    
**params**:  不分页，无参数   
**response**:  
```python
{
    valid_channels: ['ali', 'wx'],  # IOS客户端判断数组第一个值是否是apple来决定使用苹果支付还是支付宝和微信。
    items: [
        {
         "id": 3,
         "amount": 3,  # 月数
         "price": 12900,  # 按分计算，注意，所有与RMB相关的单位，都是按分传递
         "desc": "优惠50%以上",
        }
    ]
}
```

## VIP商品列表v3
**url**:  /m_mall/product/vips   
**method**:  GET    
**params**:  不分页，无参数   
**response**:  
```python
{
    valid_channels: ['ali', 'wx'],  # IOS客户端判断数组第一个值是否是apple来决定使用苹果支付还是支付宝和微信。
    banner: "fdd3fdaefa",  # 页面顶部的图片url，加密后的七牛key
    items: [
        {
         "id": 3,
         "icon": 'dwvadefefda', # 显示的图标url, 加密后的key
         "title": "1个月",  # 标题描述
         "price": 12900,  # 按分计算，注意，所有与RMB相关的单位，都是按分传递
         "descs": ["返100元话费", "永久免费通话"]
        }
    ]
}
```

## 超级VIP商品列表
**url**:  /m_mall/product/super_vips   
**method**:  GET    
**params**:  不分页，无参数   
**response**:  
```python
{
    valid_channels: ['ali', 'wx'],  # IOS客户端判断数组第一个值是否是apple来决定使用苹果支付还是支付宝和微信。
    items: [
        {
         "id": 3,
         "icon": 'dwvadefefda', # 显示的图标url, 加密后的key
         "title": "1个月",  # 标题描述
         "price": 12900,  # 按分计算，注意，所有与RMB相关的单位，都是按分传递
         "descs": ["返100元话费", "永久免费通话"]
        }
    ]
}
```

## 购买商品
**url**:  /m_mall/product/purchases      
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| product_id | int | 是 | 商品ID |
| product_type | string | 是 | 商品类型，可选值coin，vip |
| channel | string | 支付渠道 | 可选值,wx(微信), ali(支付宝) |

**response**:
```python
{
  "proof": "a=1&b=2&sign=fdcvadfefda",  # 支付凭证
}
```
> 支付凭证proof说明：
 如果支付渠道是ali支付宝，返回客户端直接用来调起支付宝支付的字符串；如果渠道是wx微信，返回[这个文档](https://pay.weixin.qq.com/doc/api/app/app.php?chapter=9_12&index=2)中的字段组成的json字符串；

## 生成订单
**url**:  /m_mall/product/create_order      
**method**:  POST    
**params**:  

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| product_id | int | 是 | 商品ID |
| product_type | string | 是 | 商品类型，可选值coin，vip |
| channel | string | 支付渠道 | 可选值,wx(微信), ali(支付宝) |

**response**:
```python
{
  "order_no": "a=1&b=2&sign=fdcvadfefda",  # 订单号
  "trans_amount":"59",  # 订单金额
  "subject":"1个月会员",  # 支付标题
}
```
> 接口说明：
 该接口用于与渠道合作，接入渠道支付时生成订单的接口

## Apple应用内购买
**url**:  /m_mall/product/iap_purchases   
**method**:  POST      
**params**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| product_id | int | 是 | 商品ID |
| product_type | string | 是 | 商品类型，可选值coin，vip |
| receipt | string | 是 | apple返回的凭证 |

**response**:
```python
{
  "result": "SUCCESS",   # 一般是SUCCESS, 异常是FAIL
}
```

## apple应用内购买恢复vip
**url**:  /m_mall/iap_vip_restore   
**method**:  POST      
**params**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| receipt | string | 是 | apple返回的凭证 |

**response**:
```python
{
  "result":  true, # 为true恢复成功， 刷新即可有会员身份。 为false表示失败。
}
```

## 微信支付失败返回码统计
**url**:  /m_mall/wx_failure   
**method**:  POST      
**params**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| err_code | int | 是 | 微信支付的返回码 |

**response**:
```python
{}
```

## 支付结果统计（用于核对第三方支付）
**url**:  /m_mall/pay_result   
**method**:  POST      
**params**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| result | bool | 是 | True成功 False失败 |
| proof | string | 是 | 支付凭证（使用图片资源加密的方式） |
| channel | string | 是 | 'ali', 'wx' |

**response**:
```python
{}
```
