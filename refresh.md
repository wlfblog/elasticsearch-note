- 手动执行index refresh，refresh目的是为了新index的数据可以被ES搜索。
```
curl -XPOST 'http://localhost:9200/kimchy,elasticsearch/_refresh'
curl -XPOST 'http://localhost:9200/_refresh'
```


- 修改定时refresh间隔
```
curl -XPUT 'localhost:9200/session_log_20160825/_settings?pretty' -d '{
    "index" : {
        "refresh_interval" : "5s"
    } 
}'
```
