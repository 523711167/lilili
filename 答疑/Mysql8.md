### Mysql8.4

###### Mysql8.4密码重置

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

###### Mysql8.4密码重置第二种方法

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
> 👀 kip-grant-table 表示mysql启动之后，跳过权限表单的验证，任何人可以登录mysql

