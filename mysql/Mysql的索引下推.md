### Mysql的索引下推

Mysql服务层将where条件中部分索引列推送到Innodb存储引擎层进行过滤,减少回表操作,进而减少返回给Mysql服务层的数据.

```sql
CREATE INDEX idx_name_age ON user1 (name, age);
EXPLAIN SELECT * FROM user1 WHERE name = 'lala' AND age > 18;
Using index condition
```

