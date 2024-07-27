### Spring Starter

​	Spring Starter被称为启动器，只需要在pom引入对应的启动器，读取spring.factories文件，获取配置全限定类名，Springboot就可以读取xxxAutoConfiguration配置类，根据配置类的conditional条件和对应注解实例化Bean。

> 原SpringMvc的环境下，
>
> 首先需要在we b.xml中配置URL映射
>
> 然后配置springmvc-servlet.xml的视图解析器、映射器，处理器
>
> 最后还需要在application-context.xml中引入springmvc-servlet.xml
>
> 事物管理、数据库链接等等配置

