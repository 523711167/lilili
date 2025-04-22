# Docker启动elasticsearch

###### docker启动

```shell
docker run -d \
		--name es \
    -e "ES_JAVA_OPTS=-Xms512m -Xmx512m" \
    -e "discovery.type=single-node" \
    -v /home/es-data:/usr/share/elasticsearch/data \
    -v /home/es-logs:/usr/share/elasticsearch/logs \
    -v /home/es-plugins:/usr/share/elasticsearch/plugins \
    --privileged \
    --network es-net \
    -p 9200:9200 \
    -p 9300:9300 \
elasticsearch:7.12.1
# -v /home/es-data:/usr/share/elasticsearch/data：挂载逻辑卷，绑定es的数据目录
# -v /home/es-logs:/usr/share/elasticsearch/logs：挂载逻辑卷，绑定es的日志目录
# -v /home/es-plugins:/usr/share/elasticsearch/plugins：挂载逻辑卷，绑定es的插件目录
# -p 9200:9200 Elasticsearch 的 HTTP REST API 端口
# -p 9300:9300 Elasticsearch 的传输通信端口,用于集群内部通信,节点间使用这个端口形成集群并同步数据
```

###### kibana启动

```shell
docker run -d \
--name kibana \
-e ELASTICSEARCH_HOSTS=http://172.17.0.3:9200 \
-p 5601:5601  \
kibana:7.17.28

```



