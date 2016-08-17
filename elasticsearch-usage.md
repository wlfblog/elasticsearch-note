
## ElasticSearch 相关配置和优化
 查看索引的setting  
```
curl -XGET 'host:9200/test/settings?pretty'
```
- 查看集群的setting  
```
curl -XGET 'host:9200/cluster/settings?pretty'
```
- 修改索引的副本数  
```
curl -XPUT 'host:9200/test/_settings?pretty' -d '{
"index" : {
"numberof_replicas" : 1
}
}'
```
- 修改索引的返回最大值  
```
curl -XPUT 'host:9200/testobject/settings?pretty' -d '{
"index.max_result_window" : 1000
}'
```
- 设置对存储进行限流 默认是20mb 增加es写入性能  
```
curl -XPUT 'host:9200/cluster/settings?pretty' -d '{
"persistent" : {
"indices.store.throttle.maxbytes_per_sec" : "100mb"
}
}'
```

## Elasticsearch templates使用  
**描述**  
- elasticsearch mapping定义未知字段类型  
  
**流程**  
- 创建索引  
```
 curl -XPUT 'host:9200/tests?pretty'
```
- 添加模板  
```
curl -XPUT 'host:9200/tests/t/_mapping?pretty' -d '{
	"dynamic_templates" : [{
		"test" : {
			"match" : "*",
			"match_mapping_type": "string",
			"mapping": {
				"type" : "string",
				"index" : "not_analyzed"
			}
		}
	}]
}'
```
- 插入数据  
```
curl -XPUT 'host:9200/tests/t/2?pretty' -d '{
	"aaa" : "aa bb"
}'
curl -XPUT 'host:9200/tests/t/1?pretty' -d '{
	"bbb" : 100
}'
```

- 查看mapping  
```
{
  "tests" : {
    "mappings" : {  
      "t" : {
        "dynamic_templates" : [ {
          "test" : {
            "mapping" : {
              "type" : "string",
              "index" : "not_analyzed"
            },
            "match" : "*",
            "match_mapping_type" : "string"
          }
        } ],
        "properties" : {
          "aaa" : {
            "type" : "string",
            "index" : "not_analyzed"
          },
          "asas" : {
            "type" : "string",
            "index" : "not_analyzed"
          },
          "bbb" : {
            "type" : "long"
          }
        }
      }
    }
  }
}
```
- 查询  
```
curl -XPOST 'host:9200/tests/t/_search?pretty' -d '{
	"size" : 0,
	"aggs" : {
		"test" : {
			"terms" : {
				"field" : "aaa"
			}
		}
	}
}'
```

