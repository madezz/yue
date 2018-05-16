# 数据库的索引、事务和锁
[主页](Home.md)->[服务器主页](server-team.md)->[学习分享](learn-and-share.md)

## 索引

> 索引相关的好文章: [MySQL索引背后的数据结构及算法原理](http://blog.codinglabs.org/articles/theory-of-mysql-index.html)

**索引很重要**

* 搜索索引平均低于logn的时间复杂度
* 按没有索引的字段的字段查询，是在全表扫描。
* 按没有索引的字段update和delete，有锁全表的过程

**怎么建索引**

* 记录少的表不用建索引
* [选择性]不高的字段不用建索引(用户)    / 100000000
* 字段查询频率高的要建索引
* 联合索引, 最左前缀匹配原则

**mysql中默认建索引的行为**

* 外键
* 唯一键

### 事务和锁





