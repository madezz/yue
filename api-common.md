# 公共接口
[主页](Home.md)->[服务器主页](server-team.md)->[接口主页](api-doc.md)

## 获取七牛上传token
> 由于我们应用上传图片的场景不多，建议客户端在注册时尽量少的请求token。（token有过期时间、token会在服务器数据库留存，太多不用会造成冗余）

**url**: common/upload_tokens  
**method**: GET  
**params**:    

|  参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| num | int | 是 | 一次性获取的token个数 |
| res_type | enum | 是 | 资源的类型，可选值: picture, video, audio |
**response**:
```json
{
  "tokens": [
      {
        "token": "BCE90lSQ61bW6_rKv7nQCcSlbukk6vbddXTjfb6f:I-ftPaipFB7hFVXT8OjdEeLuZBI=:eyJkZWFkbGluZSI6MTQ3Njc3MjY1Miwic2NvcGUiOiJ0Y3ktcGljdHVyZTpjMGQ0ZjkyOC1kN2Q2LTQ4ODctYTczYy1kZTQ0YTM2YjU2NjMifQ==",
        "key": "c0d4f928-d7d6-4887-a73c-de44a36b5663"
      }
]
}
```

## 获取位置信息
**url**: /common/location   
**method**:  GET  
**paras**:    

| 参数名 | 参数类型 | 是否必须 | 参数说明 |
| ---- | ---- | ---- | ---- |
| lng | float | 否 | 经度，获取不到传空 | 
| lat | float | 否 | 纬度，获取不到传空 |

```python
{
  "city": "武汉市", # 获取不到位null
}
```


## 获取APP-server协商的信息
>客户端每次被唤起时，更新此配置

**url**: /common/negotiation   
**method**:  GET  

```python
{
  "im_config": {
  "non_vip_max_hello": 10,  # 非vip一天最多的招呼数量
  "homepage_remain_time": 60,  # 在个人主页和动态停留超过60s，触发一条话术
  "post_like_count": 2,  # 对个人动态点2个赞促发被关心话术
  "msg_polling_period": 30,  # 每隔30s进行一次polling拉取数据，设置默认值为30
  "ping_interval": 30,  # 客户端ping的时间间隔，如果没取到，默认30s
  "max_replies": 2,  # IM会话的最多回复条数
},
"show_discount_products":False,
"not_in_audit":False, #用户ios审核配置，控制豆币-提现功能的显示与隐藏, 在没有取到值时默认为False
}
```


七牛测试域名（如果我们域名备案太慢，之后可能有个专门接口来协商域名）     

| 资源类型 | 域名 |
| --- | --- |
| picture | oev7wnywk.bkt.clouddn.com |
| video | oev73yoe1.bkt.clouddn.com |
| audio |  oev78dlmx.bkt.clouddn.com |
