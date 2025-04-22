### Mysql的Binlog

BinLog是mysql服务层日志文件,默认在**事务提交**前同步到磁盘([`sync_binlog=1`](https://dev.mysql.com/doc/refman/8.4/en/replication-options-binary-log.html#sysvar_sync_binlog)).

> [!CAUTION]
>
> 💡 默认保存在/var/lib/mysql/binlog.xxxx文件
>
> 💡 Mysql的数据文件保存在/var/lib/mysql/database-name/table-name文件中,包含**数据**和**表结构**以及**索引**



##### Binlog的作用

- 备份文件数据恢复  
- 从Mysql服务器同步主服务器数据

##### 如何理解提交事务前

​	客户端执行commit,Mysql需要执行很多操作以完成事务提交,比如需要写入redolog,binlog,undolog,如果Mysql崩溃,可能会出现redolog写入记录,binlog丢失对应Sql,这些都是需要恢复处理,sync_binlog=1可以理解为在commit返回客户端结果之前完成同步磁盘,或者是commit期间完成同步磁盘.

##### 如何保证Redolog和Binlog同步

​	RedoLog默认在事务提交之前写入磁盘,sync_binlog=1保证事务提交之前写入磁盘.

​	同时Mysql支持**二阶段提交**以保证Mysql崩溃时,确保Redolog和Binlog同步,恢复期间扫描Binlog文件收集事务ID,然后通知Innodb结束**准备阶段事务**,截断Binlog至最后有效位置,确保Binlog反应真实的data file.

###### binlog系统变量

```shel
# binlog同步由操作系统控制，和commit时机没有关联，在操作系统崩溃的情况下，可能会发生服务器提交的事务，但是尚未同步到binlog(Mysql的二进制日志写入操作系统的文件系统缓冲中,操作系统自行判断刷行到磁盘的时机)。
sync_binlog=0
# Mysql提交事务前,将当前事务写入系统文件缓存，立即刷新到Binlog文件(此时事务还是处于准备阶段,参见二阶段提交)
sync_binlog=1
# Mysql收集到N个事务提交组，然后刷新到Binlog日志，如果操作系统发生崩溃，Binlog会丢失当前收集的事务提交组的数据（InnoDB已经成功写入，只是Binlog需要等待N个事务提交组一起同步）。
sync_binlog=N>1
```

> [!CAUTION]
>
> 💡 Binary logging is done immediately after a statement or transaction completes but before any locks are released or any commit is done. This ensures that the log is logged in commit order.
>
>  💡早期版本即使设置sync_binlog=1，同样也会导致binlog和datafile不一致的情况，发生在Mysql服务端提交commit，binlog正常写入，再通知到InnoDB,如果发生Mysql宕机(发生在binlog正常写入，通知InnoDB阶段中间环节),重启InnoDB正常Rollback，binlog写入导致数据**不一致**，后期通过开启InnoDB支持**二阶段提交**解决。

> [!IMPORTANT]
>
> 二阶段提交解决binlog和datafile的**数据一致性**(前提sync_binlog=1)
>
> Mysql崩溃，重启后innoDB的日志会发生回滚,Mysql服务端会扫描Binlog,收集xid（事务ID）和Binlog最后有效位置，Mysql服务器告诉InnoDB写入的**准备日志事务**(二阶段提交中，参与者准备完成后，需要告知协调者结果，协调者收集所有参与者的成功反馈，在通知所有参与者提交事务)，截断到Binlog最后有效位置,保证Binlog和Datafile的一致性。

