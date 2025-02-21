## Dockerfile

dockerfile文件自定义构建镜像文件

### dockerfile文件定义

```shell
# 使用 redis 官方镜像作为基础镜像
FROM redis:lastest

# 设置维护者信息
LABEL maintainer="xiaoxipeng 523711167@qq.com"

# 设置容器内的工作目录，后续COPY RUN 命令的target目录都是/usr/src/app
WORKDIR /usr/src/app

# dockerfile目录下执行docker build -t redis:v1 . ，其中.代表宿主机当前目录为工作目录
# 复制宿主机工作目录的package.json 和 package-lock.json，到容器内的工作目录
COPY package*.json ./

# 安装依赖
RUN npm install

# 复制宿主机工作目录到容器内工作目录
COPY . .

# ADD也可以执行复制，但是如果是tar文件会自动解压.
# ADD

# 仅仅只是做端口声明
EXPOSE 3000

# 当 Docker 容器启动时，它会执行 ENTRYPOINT 中指定的命令。而且，ENTRYPOINT 是不可被覆盖的.
ENTRYPOINT ["java", "--add-opens", "java.base/java.lang=ALL-UNNAMED", "--add-opens", "java.base/java.lang.reflect=ALL-UNNAMED", "-Djava.security.egd=file:/dev/./urandom", "-jar", "app.jar"]

# 定义容器启动docker run --name redis_v1 redis:v1后，启动的CMD的命令，
# 则覆盖CMD命令，如果指定redis:v1执行的命令
CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
```

> [!CAUTION]
>
> 💡 Dockerfile的指令每执行一次都会在docker上新建一层，所以过多无意义的层，会导致镜像膨胀。
>
> 💡 ENTRYPOINT用于容器启动后执行的命令，不会被覆盖，CMD会被覆盖，如果在docker run --name redis_v1 redis:v1 ls，ls命令会覆盖cmd中的命令。

