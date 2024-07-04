### Mysql的Binlog

BinLog是mysql服务层日志文件,默认在**事务提交**前同步到磁盘([`sync_binlog=1`](https://dev.mysql.com/doc/refman/8.4/en/replication-options-binary-log.html#sysvar_sync_binlog)).

> ​	默认保存在/var/lib/mysql/binlog.xxxx文件
>
> ​    mysql的数据文件保存在/var/lib/mysql/database-name/table-name文件中,包含**数据**和**表结构**以及**索引**
>
> 

##### Binlog的作用

- 备份文件数据恢复  
- 从Mysql服务器同步主服务器数据

##### 如何理解提交事务前

​	客户端执行commit,Mysql需要执行很多操作以完成事务提交,比如需要写入redolog,binlog,undolog,如果Mysql崩溃,可能会出现redolog写入记录,binlog丢失对应Sql,这些都是需要恢复处理,sync_binlog=1可以理解为在commit返回客户端结果之前完成同步磁盘,或者是commit期间完成同步磁盘.

##### 如何保证Redolog和Binlog同步

​	RedoLog默认在事务提交之前写入磁盘,sync_binlog=1保证事务提交之前写入磁盘.

​	同时Mysql支持**二阶段提交**以保证Mysql崩溃时,确保Redolog和Binlog同步,恢复期间扫描Binlog文件收集事务ID,然后通知Innodb结束**准备阶段事务**,截断Binlog至最后有效位置,确保Binlog反应真实的data file.

