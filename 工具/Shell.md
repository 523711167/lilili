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

