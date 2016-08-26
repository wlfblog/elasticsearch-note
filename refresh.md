```
curl -XPOST 'http://localhost:9200/kimchy,elasticsearch/_refresh'
curl -XPOST 'http://localhost:9200/_refresh'
```
手动执行index refresh，refresh目的是为了新index的数据可以被ES搜索。
