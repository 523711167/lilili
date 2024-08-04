### Mysql8.4密码重置

#### 1.关闭Mysql服务

#### 2.创建脚本文件

​		ALTER USER 'root'@'localhost' IDENTIFIED BY '123qweQWE...';

> Root用户无法修改localhost为%,后期可以通过修改表信息将root的host修改为%
>
> update mysql.user set host = ‘%’ where user = ‘root’; FLUSH PRIVILEGES;
>
> 密码需要有一定的复杂度
>
> 必须确保mysql用户对脚本文件有读权限

#### 3.执行mysqld --init-file=脚本文件 --user=mysql &

> 如果使用Root用户登录Linux,创建脚本,在启动mysql必须要指定mysql用户,不然Root用户启动,文件权限有问题

#### 4.正常登陆Mysql

