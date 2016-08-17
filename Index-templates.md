## index template and dynamic_templates使用

- create templates
```
curl -XPUT 'host:9200/_template/template_1?pretty' -d '
{
  "template": "tttt*",// 匹配tttt开头的索引
  "settings": {
    "number_of_shards": 1
  },
   "mappings": {
      "my_type": {
        "dynamic_templates": [
          {
            "ooo": {
              "match":"*", 
              "match_mapping_type": "string",
              "mapping": {
                "type": "string",
                "analyzer": "not_analyzed"
              }
            }
          }
      ]
		}
	}
}
'
```
- 查看 template
```
curl -XGET 'host:9200/_template/template_1?pretty'
```
- 删除 template
```
curl -XDELETE 'host:9200/_template/template_1?pretty'
```

- 创建索引
```
curl -XPUT 'host:9200/tttt1?pretty'
```
- 查看索引的mapping
```
curl 'host:9200/tttt1/_mapping?pretty'

{
  "tttt1" : {
    "mappings" : {
      "my_type" : {
        "dynamic_templates" : [ {
          "ooo" : {
            "mapping" : {
              "analyzer" : "not_analyzed",
              "type" : "string"
            },
            "match" : "*",
            "match_mapping_type" : "string"
          }
        } ]
      }
    }
  }
}

```

[1 indices templates](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-templates.html)  
[2 dynamic templates](https://www.elastic.co/guide/en/elasticsearch/guide/current/custom-dynamic-mapping.html#custom-dynamic-mapping)  
