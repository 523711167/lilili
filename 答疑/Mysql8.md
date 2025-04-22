### Mysql8.4

###### Mysql8.4密码重置

1. Mysql8.4密码重置

```
# 1.关闭Mysql服务
# 2.创建脚本文件
	ALTER USER 'root'@'localhost' IDENTIFIED BY '123qweQWE...';
	3.执行mysqld --init-file=脚本文件 --user=mysql &
	4.正常登陆Mysql
```

> [!CAUTION]
>
> 💡  如果使用Root用户登录Linux,创建脚本,在启动mysql必须要指定mysql用户,不然Root用户启动,文件权限有问题
>
> 💡  Root用户无法修改localhost为%,后期可以通过修改表信息将root的host修改为%
>
> ​	update mysql.user set host = ‘%’ where user = ‘root’;
>
> ​        FLUSH PRIVILEGES;

2. Mysql8.4密码重置第二种方法

```
# 1.找到Mysql的配置文件，/etc/my.cnf
# 2.添加skip-grant-tables配置
# 3.重启Mysql，通过mysql直接连接
# 4.执行 FLUSH PRIVILEGES;
				ALTER USER 'root'@'localhost' IDENTIFIED BY '123qweQWE...';
#	5.退出mysql，重启mysql。			 
```

> [!TIP]
>
> 👀 FLUSH PRIVILEGES; 表示重新加载mysql的权限表，一般在update权限表后执行。
>
> 👀 skip-grant-table 表示mysql启动之后，跳过权限表单的验证，任何人可以登录mysql

###### Mysql中使用order by和limit查询异常问题

​	会出现乱序的查询，并且后续的分页中会出现重复数据,建议在order by加入唯一的排序条件。

[1]: https://blog.twjoin.com/mysql-%E4%B8%AD-order-by-%E8%88%87-limit-%E5%90%8C%E6%99%82%E4%BD%BF%E7%94%A8%E5%B0%8E%E8%87%B4%E4%BA%82%E5%BA%8F-a6a561e9830d

###### Mysql索引优化

###### Mysql的解释计划观察的参数

​	**type:** 连接类型

​	**Extra: **其他信息

​	**select_type:** 查询类型

###### Mysql的text类型可以保存大概多少个中文字符

​	UTF-8的编码情况下中文占用3个字符，text类型的大小为65,535字节，大概为2w多个字符。

###### Mysql的全文索引

​	全文索引只能创建在text char varchar类型上，内部采用倒排索引来实现的，长文本上创建全文索引，替代like查询。

> [!IMPORTANT]
>
> 倒排索引：是一种数据结构，首先分析文档中的词汇，构成词汇表,对于词汇表中的词记录在多少文档中出现,形成词到文档的映射关系，用户通过词汇查询，快速查找词汇对应的文档列表，返回结果。
>
> [1]: https://blog.csdn.net/yangbindxj/article/details/122868100

###### Mysql创建用户流程

```shell
# mysql 5
CREATE USER 'user'@'%' IDENTIFIED BY 'user';
# mysql 8 
# MySQL 8 默认使用 caching_sha2_password 插件认证，但有些客户端/框架（如某些老版本的 Navicat、JDBC）不支持它
CREATE USER 'newuser'@'%' IDENTIFIED WITH mysql_native_password BY 'StrongPassword123!';
# 授权用户
# 所有权限 在database数据库的所有表 给user用户 允许来自任何IP的网络连接
GRANT ALL PRIVILEGES ON database.* TO 'user'@'%';
# 刷新权限
FLUSH PRIVILEGES;

```

