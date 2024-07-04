### Redis的持久化

Redis的持久化分为Rdb和Rof两种方案

##### RDB方案

按照指定时间间隔对数据集进行快照,主要用于数据备份.

> 数据集很大,fork()可能会很耗时,可能会导致Redis停止服务

#### AOF方案

持久性记录服务器收到的每个写入操作命令

> AOF的文件会比同样数据集的RDB文件要大

##### AOF重写原理

redis > 7.0  父进程Fork()子进程,子进程重写**新的baseAOF文件**,父进程写入**新的increamentAOF文件**,如果重写失败,**旧baseAOF文件**和**旧increamentAOF文件**加上**新的increamentAOF文件**构成完整的数据,当子进程重写完成,通知父进程创建 mainifest文件,然后执行原子替换操作.