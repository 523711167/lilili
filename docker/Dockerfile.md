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
> 💡 CMD和ENTRYPOINT分EXEC和SHELL两种格式，EXEC格式为 ["echo", "Hello World"], SHELL格式 echo Hello World

> [!CAUTION]
>
> 💡**CMD和ENTRYPONIT单独使用**
>
> ​     CMD可以被替换的，docker run imageId echo helloworld，会替换dockerfile定义的CMD命令。
>
> ​     ENTRYPONIT是不可被替换的，除非传递--entrypoint printenv，使用printenv重写命令。

> [!CAUTION]
>
> 💡  **CMD和ENTRYPONIT混合使用**
>
> ​       当混合使用的时候，确保使用的都是EXEC格式
>
> ​       ENTRYPOINT ["echo", "HelloWorld"]
>
> ​       CMD ["wellcome xiaoxipeng "]
>
> ​       ENTRYPOINT作为instructions，CMD作为parameter，CMD可以被docker run传递的参数所改变,如果CMD中含有多个参数，	       docker run传递一个参数也会覆盖CMD中的多个参数。

