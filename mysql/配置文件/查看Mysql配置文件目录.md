### 查看Mysql配置文件目录

```shell
mysql --help | grep 'my.cnf'
```

/etc/my.cnf /etc/mysql/my.cnf /usr/etc/my.cnf ~/.my.cnf，这些就是mysql默认会搜寻my.cnf的目录，顺序排前的优先。