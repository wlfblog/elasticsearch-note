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
