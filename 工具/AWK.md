# AWK命令

AWK命令是用来格式化文本的。

## Option参数

	- F ：指定输入文本的分隔符，默认为空格。
	- -v param=1: 设置awk内部的变量值。

## 选项参数

```shell
awk options 'pattern {action}' file
```

​	pattern：匹配输入数据的模式，默认所有行数据。

​	{aciton}：模式匹配的行执行的操作，默认打印。

## 内置变量

​	NF：表示匹配的行号

## TIP

```shel
# 环境变量按照：分割后输出
echo $PATH | awk -F :  '{for(i=1; i<=NF; i++) print $i}'

```



