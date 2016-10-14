## 测试elasticsearch 关联用法之parent child

- 创建mapping
```
PUT testparent
{
  "mappings": {
    "p":{
      "_all": {
        "enabled": true
      },
      "properties": {
        "pname" :{
          "type": "string",
          "index": "not_analyzed"
        },
        "ptag" :{
          "type": "string",
          "index": "not_analyzed"
        }
      }
    },
    "c":{
      "_all": {
        "enabled": true
      },
      "_parent": {
        "type": "p"
      },
      "properties": {
        "cname":{
          "type": "string",
          "index": "not_analyzed"
        },
        "ctag":{
          "type": "string",
          "index": "not_analyzed"
        }
      }
    }
  }
}
```

- 插入测试数据

```
PUT testparent/p/2
{
  "pname" : "pn2",
  "ptag" :"pt2"
}

PUT testparent/c/2?parent=2
{
  "cname" : "cn2",
  "ctag" :"ct2"
}

```

- 查看

```
POST testparent/_search
```

- 搜索

```
POST testparent/_search
{
  "query": {
    "has_child": {
      "type": "c",
      "query": {
        "term": {
          "cname": {
            "value": "cn1"
          }
        }
      }
    }
  },
  "aggs": {
    "tagaggs": {
      "terms": {
        "field": "ptag",
        "size": 10
      }
    }
  }
}

```

