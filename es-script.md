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


- 这里有个bug

```
        String script = "shorts.contains(doc['"+type+"'].value)"; // 1
        //String script = "doc['"+type+"'].value in shorts";         // 2
        Map<String, Object> params = new HashedMap();
        Set<String> set = new HashSet<>();
        set.add("a");
        set.add("b");
        params.put("shorts", set);
        //when use script 1  "took" : 398008
        //when use script 2  "took" : 2001
        //改问题没有解决 官网的给的答案： no idea - some groovy weirdness. Groovy is deprecated. I suggest looking at the new scripting language Painless which is coming in 5.0
```  





