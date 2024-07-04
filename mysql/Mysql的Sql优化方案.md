### Mysql的Sql优化方案

执行查询时,将额外的过滤条件推送到存储引擎层进行处理,减少取出的数据行,提升查询性能.

```sql
select * from user where name = 'pdd' limit 10000000 10
查询效率极其低下,因为按照SQL执行流程,通过name查询数据,然后回表查询10000010记录,然后丢弃前10000000条数据
优化后
select * from user q inner join (select id from user qq where qq.name = 'pdd' limit 10000000 10) t on q.id = t.id 
子查询减少回表的次数,还可以通过主键查询提高效率
```

