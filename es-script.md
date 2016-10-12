- 计算分页数据的绝对位置  

```
POST /index/_search
{
  "script_fields": {
    "test": {
      "script": {
        "inline": "doc['position'].value + (doc['page_index'].value - 1) * doc['page_size'].value"
      }
    }
  }
}
```

- script params java usage

```
String[] types = {"a", "b"};
Map<String, Object> params = new HashedMap();
params.put("types", types);
String script = "doc['type'].value in types ? '1':'0'";
//agg
TermsBuilder video_type = AggregationBuilders.terms("type")
  .script(new Script(script, ScriptService.ScriptType.INLINE, "groovy", params));

//filter
.....

//scriptField
......

```


