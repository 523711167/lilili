Mysql的RedoLog

Mysql重启恢复期间,RedoLog用于修正不完整事务写入的数据.

> ​	RedoLog采用的日志先行的策略,首先Buffer Pool数据修改信息写入log buffer,**提交事务之前**(精确时间是在脏页刷新到磁盘之前)刷新到RedoLog,默认[`innodb_flush_log_at_trx_commit`](https://dev.mysql.com/doc/refman/8.4/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit)=1,满足ACID约定

#####    RedoLog作用

​	Pool buffer数据刷新磁盘发生异常(Commit期间多个脏页刷新到Data Files发生异常),恢复期间通过RedoLog的LSN码恢复.

##### Mysql commit提交流程

​	Mysql执行updete，首先会将磁盘数据加载到Buffer Pool中，修改Buffer Pool中的数据项（脏页），同时将数据修改的记录写入Log Buffer中，Commit提交Log Buffer数据写入RedoLog,脏页数据后台刷新至磁盘