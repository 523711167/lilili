### Innodb磁盘数据

​	启用innodb_file_per_table,每个表都会有自己的表空间(.ibd),数据,索引都保存在文件中

> Pdd数据库user表---->/var/lib/mysql/pdd/user.idb
>
> 如果未启用此选项，‌那么所有表的记录和索引将存储在MySQL数据目录下的共享表空间文件中，‌通常名为ibdata1