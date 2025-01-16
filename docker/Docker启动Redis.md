## Docker启动Redis

使用指定配置文件启动redis

```shell
docker run \
-v /myredis/conf:/usr/local/etc/redis \
--name myredis \
redis:lastest redis-server /usr/local/etc/redis/redis.conf \
```
