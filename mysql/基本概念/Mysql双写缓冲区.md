### Mysql双写缓冲区

脏页刷新到磁盘之前,把数据写入双写缓冲区,再刷新到磁盘,用于在 an operating system, storage subsystem, or unexpected [**mysqld**](https://dev.mysql.com/doc/refman/8.4/en/mysqld.html) process exit in the middle of a page write异常重启,找到完整的脏页备份副本恢复数据.

> ​	脏页刷新到**磁盘期间**Mysql崩溃需要备份副本恢复
>
> ​    保存在/var/lib/mysql目录 \#**ib_16384_0.dblwr**  #**ib_16384_1.dblwr**

