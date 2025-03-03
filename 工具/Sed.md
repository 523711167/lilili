# Sed

​	👀 在线编辑器，以行为单位处理数据，输出处理结果。

###### sed "s/^hostname:  .*/hostname: $host/g" -i ./harbor.yml

​	s：开启替换模式，每行以^hostname:  .*匹配的内容，替换为hostname: $host，g表示全局替换

-i表示直接修改源文件（-i 命令不会输出结果）。