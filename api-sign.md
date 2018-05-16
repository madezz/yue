# 接口反扒方案
[主页](Home.md)->[服务器主页](server-team.md)->[接口文档](api-doc.md)

>为了保护图片、视频等关键资源，以及防止爬虫消耗api资源，我们的接口将通过如下方式反扒。
* api接口签名
* 资源url加密
* 客户端代码混淆
* 数据ID混淆
* 接口调用频率限制(以后做)
* https(以后做)

## api接口签名
**所有接口**默认都要使用签名调用
每次请求API时，都要加入如下3个http request header

| Header名 | 类型 | 说明 |
| ------------- | -------| -------|
| X-Api-Nonce | string | 客户端生成一个随机字符串，如uuid |
| X-Api-Timestamp | string | 客户端根据当前时间生成timestamp(从1970来的秒数) |
| X-Api-Sign | string | 客户端根据X-Api-Nonce、 X-Api-Timestamp、X-Api-Sign生成hash值作为签名|

签名生成方法，根据客户端和服务器约定的key(`91c$)&2&_)tx^dhd+%5!nrl!47*z&xwm3_7se9kdt8j&%f0fym`)和X-Api-Nonce、X-Api-Timestamp按顺序拼接成字符串，进行 md5 哈希计算。
python示例代码如下:
```python
def gen_headers():
    sercet = "91c$)&2&_)tx^dhd+%5!nrl!47*z&xwm3_7se9kdt8j&%f0fym"
    nonce = str(uuid4())
    cur_time = str(int(datetime.now().timestamp()))
    header = {
        'X-Api-Nonce': nonce,
        ' X-Api-Timestamp': cur_time,
        'X-Api-Sign': md5((APP_SECRET + nonce + cur_time).encode()).hexdigest(),
    }
    return header
```
接口签名一定要在客户端做好**代码混淆**才有效


## 资源url加密
服务器返回的所有七牛key值，都经过AES加密，客户端需要使用key和iv值进行解密处理。使用的AES模式为`AES/CBC/PKCS5Padding`，密钥key值`25a27237-e066-4c`，解密IV为`5c27c6f6-5cb7-40`。
[java加密解密示例](http://meiyuxiuxiu.6655.la/mty-team2/snippets/1)
object-c没有试验过，参考[这篇文章](http://ios.jobbole.com/88227/)

## 客户端代码混淆
接口签名secret、资源解密算法的代码都在客户端实现，如果被反编译很容易就会被破击，客户端要调研相关方案做好代码混淆，增加破解成本。

## 数据id混淆
为了防止数据被直接遍历，数据库中的id被返回时将进行混淆处理，逻辑由服务器实现，客户端需要注意所有的id都成了`字符串`类型。



