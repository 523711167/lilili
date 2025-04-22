# Docker操作指南

## FAQ

###### docker pull openjdk:24-ea-17-slim-bullseye含义

​	24：代表小版本吧

​	ea：代表 “Early Access”，表示这个版本是预览版或者早期访问版，通常还没有完全稳定。、

​	17：代表JDK17

​	slim：代表是精简版本,去掉冗余的组件，减少体积

​	bullseye：这是基于 Debian Bullseye（Debian 的一个版本代号）的操作系统镜像。Bullseye 是 Debian 11 的代号，代表该镜像使用的是该版本的 Debian 系统作为基础镜像。

###### docker客户端配置代理

在/etc/docker/deamon.json文件中添加

```json
"proxies": {
	"http-proxy": "http://192.168.18.115:7890",
  "https-proxy": "http://192.168.18.115:7890",
  "no-proxy": "localhost,127.0.0.1"
},
# 当docker守护进程重启时候，默认会关闭运行的容器,可以通过配置达到守护进程不可用的时候，容器仍然运行,称为实时恢复。
# 开启后，当docker守护进程重启后，运行的容器不会重新启动
# 添加完成执行systemctl reload docker.service
# docker info  | grep -i live 观察是否已开启
# systemctl restart docker.service 测试是否达到效果
"live-restore": true
```

> [!CAUTION]
>
> "https-proxy": "http://192.168.18.115:7890" 代理选择的是http，选择https有问题。

###### /lib/systemd/system/docker.service文件说明

​	👀 **systemd** 服务管理系统中的一个服务单元文件，用于定义和管理 **Docker** 服务的启动、停止和其他操作。

###### 指定平台下载镜像

指定x86平台

```
docker pull roboxes/centos8:latest --platform amd64
```

###### 批量删除none的镜像

```
docker images -q --filter "dangling=true" | xargs -I {} docker rmi {}
```

###### docker客户端连接的守护进程

```
# 指定DOCKER_HOST变量
export DOCKER_HOST="tcp://192.168.18.124:2375"
```

###### 宿主机向容器拷贝文件

```shell
# 宿主机source拷贝到容器/目录 
docker cp source target:/
# docker cp kibana.yml kibana:/usr/share/kibana/config/kibana.yml
```

###### 容器打包成镜像

```
docker commit 容器ID 镜像:版本
```

###### entrypoint和command区别

- entryporint 默认不可覆盖

- command   entrypoint存在，command作为参数补充，反之，作为命令执行。

  > [!CAUTION]
  >
  > dockerfile和docker-compose都有对应的entrypoint和command，docker-compose优先级大于dockerfile，比如
  >
  > FROM ubuntu
  >
  > ENTRYPOINT ["echo"]
  >
  > CMD ["hello world"]  会被entrypiont ["ls"] command ["-l"]覆盖

###### docker重启

​	Linux环境：

​	MacOS环境：

```shell
brew services restart docker
```
