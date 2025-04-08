# WEB

###### cookies在同IP不同端口会出现覆盖的情况

​	127.0.0.1:8080 访问服务器8080，服务器返回sessionId，127.0.0.1:8081携带8080的cookies访问服务器8081,服务器没有对应session，重新生成sessionId返回给127.0.0.1:8081

###### 什么是数字证书

​	包含证书所有者的**公钥**、所有者**身份信息**和**数字签名**。

​	数字签名是CA机构使用CA的私钥对证书里面的公钥和身份信息进行了签名。

###### SpringCloudConfig的端点类

```java
org.springframework.cloud.config.server.environment.EnvironmentController
org.springframework.cloud.config.server.resource.ResourceController
```

###### RedissonLock为可重复入锁

在springboot中MVC也是由线程池执行的，可能存在问题。

###### SpringBoot循环依赖解决

通过@Lazy注解

```java
通过
@Autowired
public void setBeanA(xxxx xxx) {} 在Bean实例化后赋值
```

@ObjectFactory和@Provider延迟注入

###### @Resource 和 @Autowired区别

Autowired根据类型注入，多种类型需要配置**Qualifier** 注入

Resource 根据别名注入

###### RS256

`RS256` 是一种结合了 RSA 加密算法和 SHA-256 哈希函数的数字签名算法

###### Maven配置中scope的范围说明

```
compile 默认 编译、测试、运行都需要
runtime 测试和运行，编译不需要。生产运行时由外部提供。适用于那些在运行时需要但在编译时不需要的库，例如某些数据库驱动。
test：仅测试时需要
provided：编译和测试需要。该依赖在运行时不包含在最终的打包文件中,常用于像 Servlet API 这样的库，它们通常由容器提供，而不是打包在应用中。
```

###### Springboot 开发中Maven的scope

```
# 表示多例，每个请求都会创建新的实例
@Scope("prototype")
# 表示单例
@Scope("singleton")
```

###### Springboot 开发中Maven的optional

```
表示依赖是可选的，依赖带有optional的模块，如果不显试指定引用依赖，依赖不会传递。
```

###### 跨域资源共享（CORS）

​	域A下访问域B的资源的一种策略，允许服务器控制哪些域可以访问其资源。

###### 预检请求（pre-flight request）

​	在进行跨域资源访问的之前，会发送预请求，服务器接收到预请求后返回跨域允许的请求头，浏览器根绝请求头的信息，决定是否发送后续请求。

> [!CAUTION]
>
> 💡   Access-Control-Allow-Origin：指定哪些域可以访问资源。
> 	Access-Control-Allow-Methods：指定允许的方法（GET、POST 等）。
> 	Access-Control-Allow-Headers：指定允许的请求头。

###### 如何判断是否存在内存泄漏的情况

​	首先内存泄漏发生堆区，通过jstat -gc的命令周期性采集jvm的指标，通过对比老年代的内存使用量，如果一直是持续增长，则说明存在内存泄漏的问题。

###### 如何判断是否存在死锁的情况

​	通过jstack pid命令，输出当前jvm进程中的线程快照，观察输出线程的状态，重点观察有无deadlock、blocked、wait condition、wait minitor状态的线程。

###### 如何定位CPU**飙升**的问题

​	首先CPU飙升常见于，多线程任务限于死循环中、同步IO操作使用不当,涉及大量计算和加解密过程

	1. 使用TOP命令查看CPU占用高进程ID.
	1. 通过top -Hp 进程ID，找到CPU最高的线程ID
	1. 在通过Jstack打印当前进程运行的线程快照
	1. 找到对应线程的执行状态，观察是否线程陷入blocked，和执行代码块。

> [!CAUTION]
>
> 💡同步IO操作使用不当常见见于频繁打开关闭文件、大文件对象读取不使用缓冲区、网络API请求大量被阻塞。

