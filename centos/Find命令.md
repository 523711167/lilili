# Find命令

## FAQ

###### 查找conf目录

```
# / 从根目录查询
# -type d 限制结果返回目录
# -type f 限制结果返回文件
# -name cond 查找目录名称conf
#	-iname 忽略大小写
find / -type d -name "conf"
```

