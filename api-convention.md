# 接口约定于规范
[主页](Home.md)->[服务器主页](server-team.md)->[接口文档](api-doc.md)

# 关于返回列表
返回数据最外层为list时，一律使用key值为items

# 关于分页
分页一律传cursor, offset, limit三个参数， 返回值为cursor, items。  客户端请求到items长度为0时，意味着没有数据了。
