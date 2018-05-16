facelive
========

##  版本说明

依赖库|版本
---|-----
python|3.5
django|1.11.1
PyMySQL|0.7.11

+ PyMySQL为MySQL的数据库驱动。

## 安装说明

### 安装虚拟环境

1. 安装virtualenv，`pip3 install virtualenv`
2. 进入代码根目录，创建虚拟环境: `virtualenv --always-copy -p python3 venv`
3. 进入虚拟环境，安装相关依赖:

```
source ./venv/bin/activate
pip install -r requirements.txt
```

### 配置数据库

1. 运行`mysql -u root -p < scripts/init.sql`命令，创建相关的数据库
2. 添加`secret.ini`文件，将`script/secret.ini`文件复制到代码根目录下，并修改其中的数据库设置，设置好本地的数据库用户名密码等设置
3. 执行`python manage_api.py migrate`命令，同步数据库

### 运行程序

1. 执行`python manage_api.py runserver`命令，启动开发服务器


