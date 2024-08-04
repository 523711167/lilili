### Mysql元数据库概念

> 从数据库创建的信息库,用于复制过程,副本的连接元数据存储库和应用器元数据存储库统称为复制元数据存储库

##### The replica's *relay log*(中继日志)

​	由从数据库I/O线程写入,包含从源BinLog读取的事物.

##### replica's *connection metadata repository*(连接元数据存储库)	

​	从数据库接收线程从源Binlog检索的事物信息,连接源数据库的信息.

##### replica's *applier metadata repository*(应用器元数据存储库)

​	从数据库应用线程从中继日志读取和应用的信息.

