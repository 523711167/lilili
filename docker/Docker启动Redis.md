## Docker启动Redis

使用指定配置文件启动redis

```shell
docker run \
-v /myredis/conf:/usr/local/etc/redis \
--name myredis \
redis:lastest \
redis-server /usr/local/etc/redis/redis.conf \
```

**注意：**redis-server /usr/local/etc/redis/redis.conf 表示启动容器后执行的命令。

## FAQ

###### Redis配置文件模板

[1]: https://redis.io/docs/latest/operate/oss_and_stack/management/config/

###### Redis配置文件说明

[1]: https://blog.csdn.net/m0_66011019/article/details/143713762

