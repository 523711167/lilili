# WEB

###### cookies在同IP不同端口会出现覆盖的情况

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
runtime 测试和运行，编译不需要。生产运行时由外部提供。比如servlet相关API，运行在Tomcat容器中，打包不需要引入Tomcat相关jar，但是开发环境你可能有引入，还有比如开发环境你使用logback，但是运行环境有别的日志实现框架。
test：仅测试时需要
provided：编译和测试需要。
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
