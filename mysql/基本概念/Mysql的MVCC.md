Mysql的MVCC

MVCC(多版本并发控制),在多事务情况下，数据库不通过加锁方式,解决并发读写冲突问题,同时还解决不同事物数据可见性的问题，提高数据库性能.

> Mysql通过UndoLog,一致性视图,数据库表隐藏字段实现MVCC机制,控制不同事务之间数据可见性(ACID的隔离性)

##### 数据库表隐藏字段

Mysql数据表默认自动创建三个隐藏字段

- DB_ROW_ID

  隐藏的默认主键

- DB_TRX_ID

  自动递增事务ID,记录修改当前行的事务ID

- DB_ROLL_PTR

  回滚指针,指向数据行的上个版本数据(保存在undolog)

##### UndoLog

记录历史版本的数据行

##### 一致性视图

事务开启同时创建一致性试图,记录当前活跃事务ID,快照读(select)通过当前事务ID,活跃事务ID,数据行记录事务ID,判断数据对事物的可见性.

[1]: https://blog.csdn.net/error_log7/article/details/144675072

