

### Docker启动Mysql

```shell
#/var/lib/mysql 数据存放默认目录
docker run -d --name mysql \
-p 3306:3306 \
-v /root/data:/var/lib/mysql \
-e MYSQL_ALLOW_EMPTY_PASSWORD=yes \
mysql:latest
```

