# 应用服务器第一次配置手记
[主页](Home.md)->[服务器主页](server-team.md)->[线上环境](dev-deploy-doc.md)

* 安装python3.5

```
sudo add-apt-repository ppa:fkrull/deadsnakes
sudo apt-get update
sudo apt-get install python3.5
```


* 豆瓣pip镜像，安装virtualenv

```
~/.pip/pip.conf
[global]
index-url = http://pypi.douban.com/simple

virtualenv .env --python=python3.5
alias pip='pip --trusted-host pypi.douban.com'
```

* pip装msyql-client

```
直接装报错OSError: mysql_config not found
sudo apt-get install libmysqlclient-dev
继续会报error: command 'x86_64-linux-gnu-gcc' failed with exit status 1
sudo apt-get install python3.5-dev
```

* redis docker

```
db-redis:  sudo docker run --name db-redis -v /data/redis-data:/data -p 6380:6379 -d redis redis-server  --appendonly yes
hot-redis:  sudo docker run --name hot-redis -p 6379:6379 -d redis
```

* rabbitmq

```
echo 'deb http://www.rabbitmq.com/debian/ testing main' | sudo tee /etc/apt/sources.list.d/rabbitmq.list
wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc |
        sudo apt-key add -

sudo apt-get update
sudo apt-get install rabbitmq-server

sudo rabbitmqctl add_user yueroot rootmima1234
sudo rabbitmqctl set_user_tags yueroot administrator
sudo rabbitmqctl set_permissions yueroot ".*" ".*" ".*"
```
