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

Resource 更具别名注入