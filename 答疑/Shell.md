#### Shell 参数

###### **短选项**和长选项

​	-H 表示简写 等效于 --host list

###### 判断文件是否存在

```shell
if [ -f *.tar.gz ]
then
    h2 "[Step $item]: loading Harbor images ..."; let item+=1
    docker load -i ./harbor*.tar.gz
fi
echo ""
```

###### 判断字符串或者变量是否有值

```shell
if [[ -n "$HARBOR_BUNDLE_DIR" ]]; then
		harbor_prepare_path=$HARBOR_BUNDLE_DIR
else
		harbor_prepare_path="$( cd "$(dirname "$0")" ; pwd -P )"
fi
echo "prepare base dir is set to ${harbor_prepare_path}"
```

###### 权限赋予问题

```shell
# -R 表示递归赋予权限
chmod 777 -R /home
```

###### systemctl启动查看日志

```shell
# 显示 Redis 服务的最近 50 行日志
journalctl -u redis --no-pager -n 50
```

###### 压缩文件通过排除某些文件夹

```shell
# ./表示相对目录，取决于你的工作目录 也可以使用/home/xiaoxipeng 解决目录
tar --exclude='./back-log' \
    --exclude='/log' \
    -czvf backup.tar.gz /*
# -c 表示创建新的归档文件
# -v 表示显示详细过程
# -z 使用gzip压缩
# -f 指定文件名
```

###### Top命令交互操作

```
e 改变任务区域单位 bit -> mb -> gb
E 改变摘要区域单位 bit -> mb -> gb
```

