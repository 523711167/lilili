### RabbitMq的channel信道Qos

> 经过我测试,Qos代表当前信道Unacked消息数量,达到预设值,消费者**不接收消息**.
>
> channel.basicConsume代码负责**处理业务和发送消费确认**,消息**接收**成功自动判断.
>
> 可以说明我在消费者代码上打断点不执行,但是chanel信道上unacked消息持续增长

##### ready状态和unacked状态

- ready 

  表示生产者发送消息给队列,并且消息已经被队列的确认.

  > **详细过程**生产者发送消息给队列,队列通知生产者返回sequenceNumber参数,生产者通过sequenceNumber处理业务逻辑,再通知队列,此时队列的消息状态为ready,如果没有开启发布确认机制这个确认过程是透明的

- unacked

  表示消息被消费者成功接收(接受成功与否,Rabbitmq代码判断的)但未被消费者ack确认.

  > **详细过程**队列发送消息给消费者,消费者返回给队列接收成功,如果规定时间没有收到确认,再次发送给消费者,这个过程是透明的.

##### 队列对应对个消费者是如何消费的

​	多个消费者会按次序消费

##### 队列对应对个消费者,如果其中一个消费者拒绝响应,设置重新入队

​	按次序被下一个消费者消费

**如何防止RabbitMq重复消费**

> ​	生产者发送消息,网络延迟,未收到broken确认,重复发送消息.
>
> ​	消费者处理消息发生故障,或发送ack确认网络故障未送达,消息被消费者重复消费.

1. 保证消费者接口幂等性,及时重复消费也不会导致状态不一致.
2. 消息的发布确认机制,记录发送成功的消息
3. 使用RabbitMq事务机制,确认消息发送成功

#####  如何防止RabbitMq消息丢失

>    RabbitMq崩溃,信息未持久化,导致消息丢失
>
> 交换机路由消息失败,找不到路由
>
> 针对TTL到期,队列长度溢出,

1. 生产者发送消息设置mandatory=true同时注册监听函数,路由失败通知生产者处理.

2. 针对TTL到期,队列长度溢出,拒绝应答同时拒绝重新入队,队列上设置死信交换机处理.
3. 队列,消息,交换机持久化配置.