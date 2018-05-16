# 测试服务器配置手记
[主页](Home.md)->[服务器主页](server-team.md)->[线上环境](dev-deploy-doc.md)

* 将uwsgi从docker中迁出

```
1. 安装python3.5：安装python3.5解决了python3.4文件循环引用的问题
sudo add-apt-repository ppa:fkrull/deadsnakes
sudo apt-get update
sudo apt-get install python3.5

2.创建虚拟环境：
virtualenv .env --python=python3.5

3.安装uwsgi之前应当安装python的依赖
sudo apt-get install python3.5-dev

4. source之后安装uwsgi

5. uwsgi的配置文件在:~/uwsgi/api.ini console.ini中，配置文件中的路径需要全部路径，由于登录用户的不同相对路径会出错
    配置文件中设置了uwsgi对应的项目启动入口、Django环境变量等等

```


* docker中的redis

```
1. 配置redis：
db-redis:  sudo docker run --name db-redis -v /data/redis-data:/data -p 6380:6379 -d redis redis-server  --appendonly yes
hot-redis:  sudo docker run --name hot-redis -p 6379:6379 -d redis

2. 查看和启动redis
sudo docker ps 
sudo docker start db-redis
sudo docker start hot-redis

暂时不将redis迁出
```

* supervisor

```
1. 安装superviors

2. 配置superviors，配置文件目录：/etc/supervisord.conf

[program:celery_beat]
command=/home/yue/.env/bin/celery -A server_console beat
environment=DJANGO_SETTINGS_MODULE="server_console.settings.test"       ; process environment additions (def no adds)
directory=/home/yue/workspace/yue            ; directory to cwd to before exec (def no cwd)

server_console:表示wsgi的目录，即启动的入口
environment:由于要条用DJANGO，所以要给出DJANGO的环境变量配置
command：当用supervisorctl status查看，如果有task FATAL ，则可以进入到directory下，执行command查看具体的错误

```

* flower

```
1. flower的默认端口为5555

2. 使用flower查看当前tasks是否正常，目前配置的最大进程数是8，若果显示为8则表示tasks有问题

```

* mysql

```
1.sudo apt-get install mysql-server (装了server之后client也装好了)

2. 安装mysql-server失败并报错的解决方案：http://blog.csdn.net/gatieme/article/details/52839814

3. mysql进入命令：mysql -uroot -p

4. 数据库迁移 
    导出：mysqldump -u root -p rootmima -h (ip) -P (port) --database yue > yue.sql
    导入：mysql -u root -prootmima -e "source yue.sql"

5. warning: mysql语句后面需要加 ';'

```

