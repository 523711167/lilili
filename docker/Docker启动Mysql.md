

### Docker启动Mysql

> [!CAUTION]
>
> 💡国内被墙，很多镜像站不能使用，通过/etc/docker/daemon.json设置代理。

```shell
#/var/lib/mysql 数据存放默认目录
docker run -d --name mysql \
-p 3306:3306 \
-v /Users/xixipeng/Documents/mysql/conf/:/etc/mysql/conf.d/ \
-v /Users/xixipeng/Documents/mysql/init-sql/:/docker-entrypoint-initdb.d/ \
-v /Users/xixipeng/Documents/mysql/data/:/var/lib/mysql \
-e MYSQL_ALLOW_EMPTY_PASSWORD=yes \
mysql:latest 
# mysqld 启动mysql命令
# -e MYSQL_SSL=DISABLED
```

> [!CAUTION]
>
> 💡 Mysql8版本配置文件/etc/my.cnf在此目录
>
>  💡环境变量区分大小的



### 启动环节

通过docker下载mysql镜像。

启动Mysql，准备好配置文件、本地数据目录、准备初始化脚本。

通过客户端连接Mysql,修改默认的root用户密码。

创建新用户，及作权限分配。

###### 创建用户

```shell
# %            允许来自任意IP地址连接
# xiaoxipeng01 密码
create user 'xiaoxipeng'@'%' identified by 'xiaoxipeng01';
```

###### 创建database

```shell
CREATE DATABASE db;
```

###### 授权

```shell
# GRANT ALL PRIVILEGES 给予 增删改查的权限
# *.*                  给予 db数据库任意表的权限
# IDENTIFIED BY 'root' 修改密码
# WITH GRANT OPTION;   给予 授予用户权限的权限
GRANT ALL PRIVILEGES ON db.* TO 'root'@'%' WITH GRANT OPTION;
```

###### 无法连接Mysql服务器

👀 本机mysql客户端可以连接，除本机外无法连接。

1. bind-address未绑定*、0.0.0.0
2. 未关闭SSl，SHOW VARIABLES LIKE '%ssl%';查看

