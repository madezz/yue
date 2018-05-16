# 接口说明
[主页](Home.md)->[服务器主页](server-team.md)->[接口文档](api-doc.md)

## 关于rest
服务器接口按照rest风格定义
* url风格为 `http://domain.com/m_user/users`，m_user代表module user(用户模块)，users是具体的资源名。
* POST方法新增资源，PUT方法全量修改资源，PATCH方法增量修改资源
* 使用JSON传输数据，注意Content-Type为`application/json`

> 关于PATCH方法的引入
在我们上个项目中，PUT方法在修改资源时经常语义不清，比如不传字段时，是代表不修改资源，还是把资源修改为空？
把PATCH方法引入后，PUT方法不传的字段，含义是该字段设为null，如果想增量的修改一个资源（比如一次请求只需修改用户照片），使用PATCH方法。使用PATCH方法时，所有的参数都不是必填字段

## 必须的http头
客户端所有的请求都必须加上以下http request headers
* X-Api-Version：api的版本，格式为v1, v2, v3
* X-Device-ID：客户端获取到的device id
* X-App-Code：该客户端的代码，暂时传为tcy
* X-Channel-ID：渠道id，暂时传initial
* X-App-version：该App的release版本号，由客户端自己定义，例如Android/1.1, iOS/1.2。   

以及以下签名header，见[api签名文档](http://meiyuxiuxiu.6655.la/mty-team2/wikis/api-sign#api%E6%8E%A5%E5%8F%A3%E7%AD%BE%E5%90%8D)
* X-Api-Nonce
* X-Api-Timestamp
* X-Api-Sign

## 关于JSON
项目使用JSON作为数据传输格式，JSON的优势有
* 格式更灵活，能够表示更加负责的数据结构，比如嵌套的数据格式
* JSON在表示数组时更加省空间，使用www-form格式表示数组a=[1,2,3,4]，在body中为: a=1&a=2&a=3&a=4，而在JSON中为{"a": [1,2,3,4]}

## 接口返回示例
```json
{
  "status": 200,
  "message": "ok",
  "data": {}
}
```
接口的实际数据全部在data里面，以后的接口文档将省略此公共结构，只撰写data的内容。

## 错误码
* 600 ~699的错误是系统级别的错误码，客户端需要完全外抛给用户。
> 包括【版本太低，请升级】、【系统正在维护，请稍后再试】等等

* 700 ~ 799的错误码是一般的全局错误码，其中777为参数错误。

* 1000以上的错误码都是各个业务模块的错误码
