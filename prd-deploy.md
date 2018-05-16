# 应用服务器配置
[主页](Home.md)->[服务器主页](server-team.md)->[线上环境](dev-deploy-doc.md)


### uwsgi配置
api的配置文件: /home/deploy/uwsgi/api.ini   
console的配置文件： /home/deploy/uwsgi/console.ini   
[官方配置文档](https://uwsgi-docs.readthedocs.io/en/latest/Options.html)   

部分参数解释
* touch-reload: 此文件的"最后修改时间"发生改变时(被touch, 被修改)，uwsgi自动reload。
* socket: 指定uwsgi向外暴露的网卡和端口。nginx的配置会用到.
* max-requests：某worker请求量达到这个值时，reload此worker
* lazy-apps: 从每个worker启动django app。（否则从master启动，会导致共享文件句柄，在一些使用socket的情况中有线程安全问题)

### crontab定时任务
执行crontab -e进入定时任务编辑，目前有一个自动30分钟重启celery_task的定时任务。

### supervisor进程管理
配置文件: /etc/supervisord.conf  

目前配置了六个进程，一个进程组   

* log-consumer: 消费日志脚本
* errorwarning_api：api日志报警脚本
* errorwarning_console: console日志报警脚本
* tornado: 控制台推送相关进程
* flower: celery的管理控制台
* celery_beat: celery的周期性和定时任务
* 【进程组】celery_task： celery的任务进程

##### supervisor几个常用命令  

supervisorctl status: 进程执行状态   
supervisorctl update: 修改配置后更新   
supervisorctl restart/start/stop <process_name> : 重启/启动/停止进程  


### redis
热点缓存实例(hot-redis): sudo vi /etc/redis/hot-redis.conf    
持久化实例(db-redis): sudo vi /etc/redis/db-redis.conf
### RabbitMQ
