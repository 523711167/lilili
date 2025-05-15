###### ElasticSearch索引的基本操作

- 创建索引

  ```sql
  PUT /index_name
  {
  	"setting": {
  		//索引相关设置
  	},
  	"mappings":{
  		"properties": {
  			//字段属性
  			"name": {
  				"type": "text"
  			},
  			"age": {
  				"type": "integer"
  			}
  		}
  	},
  }
  ```

- 删除索引

  ```sql
  DELETE /index_name
  ```

- 查询索引

  ```sql
  # 查询索引
  GET /index_name
  # 查询
  GET /index_name/_search
  {
  	"query": {
  		// 查询条件
  	}
  }
  # 复杂查询
  POST 
  ```

- 修改索引

  ```sql
  # 修改索引相关设置
  PUT /index_name/_settings
  # 修改索引字段属性
  PUT /index_name/_mapping
  ```

###### ElasticSearch查询基本操作

```
# match_all 使用
GET /index_name/_search
{
	"query": {
		// 查询所有数据,默认从0位开始，返回10条数据
		"match_all": {}
	},
	"from": 0,
	"size": 10,
	// 设置排序字段
	"sort": [
		{
			"age": "desc"
		}
	],
	// 查询指定的filed
	"_source": [
		"name",
		"age"
	]
}


# term精确匹配
GET /index_name/_search
{
	"query": {
		"term": {
			"name": {
				"value": "lisi"
			}
		}
	}
}
# 全文检索
GET /index_name/_search
{
	"query": {
		"match": {
			"address": "友谊路98号"
		}
	}
}
# 范围查找
GET /index_name/_search
{
	"query": {
		"range": {
			"age": {
				"gte": 20,
				"lte": 26
			}
		}
	}
}
```

###### ElasticSearch关联关系

 
