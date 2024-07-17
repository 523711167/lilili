### Docker启动RabbitMQ

```shell
docker run -id --name=rabbitmq \
  -p 5671:5671 \
  -p 5672:5672 \
  -p 4369:4369 \
  -p 15671:15671 -p 15672:15672 \
  -p 25672:25672 \
  -e RABBITMQ_DEFAULT_USER=pxx \
  -e RABBITMQ_DEFAULT_PASS=123456 \
  rabbitmq:latest
```

- **5671和5672**: 这些是AMQP（高级消息队列协议）端口。5671用于启用TLS（传输层安全）的安全连接，而5672是非TLS连接的默认端口。
- **4369**: 这是Erlang Port Mapper Daemon (EPMD)端口。EPMD用于RabbitMQ集群中节点之间的发现。
- **15671和15672**: 这些端口用于通过HTTPS（15671）和HTTP（15672）访问RabbitMQ管理界面。它们提供了监控和管理RabbitMQ的管理仪表板。
- **25672**: 此端口用于Erlang分布，并且通常用于RabbitMQ集群内部节点之间的通信。

**开启界面插件**

```shell
rabbitmq-plugins enable rabbitmq_management
```