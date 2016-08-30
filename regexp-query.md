## 场景  
精确查找包含输入词,因为es查询基于term查找的，所欲要匹配的字段需要设置不分词，这样整个字段就是一个term了。

- 创建索引时 自定不分词
```
curl -XPUT "http://host:9200/test?pretty" -d '
{
	"settings" : {
		"number_of_shards" : 1,
		"number_of_replicas" : 0
	},
	"mappings" : {
		"estype" : {
			"properties" : {
				"name" : {
					"type":"string",
					"index":"not_analyzed"
				}
			}
		}
	}
}'
```
## 实现方式
### 正则表达式
- java查询  
```
public void containQuery(String input){
    String query = ".*" + input + ".*";
    SearchResponse searchResponse = client.prepareSearch("test").setTypes("estype").setQuery(QueryBuilders.regexpQuery("name",query)).get();
    System.out.println(searchResponse);
}
```

- rest查询  
```
curl -XPOST 'host:9200/test/_search?pretty' -d '{
  "query" : {
    "regexp" : { "name" : ".*你好北.*" }
  }
}'
```

### 通配符
- rest查询  

```
curl -XPOST 'host:9200/test/_search?pretty' -d '{
  "query" : {
    "wildcard" : { "name" : "*你好北*" }
  }
}'  
```

- sql sql插件支持该类型
```
select * from test where name like '*好北%'
```


- 其他用法见官网  
[https://www.elastic.co/guide/en/elasticsearch/reference/2.3/query-dsl-regexp-query.html](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/query-dsl-regexp-query.html)
