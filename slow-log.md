- 设置search log
```
curl -XPUT 'host:9200/session_log_20160825/_settings?pretty' -d '{
	"index" : {
		"search.slowlog.threshold.query.warn": "10s",
		"search.slowlog.threshold.query.info": "5s",
		"search.slowlog.threshold.query.debug": "2s",
		"search.slowlog.threshold.query.trace": "500ms",
		"search.slowlog.threshold.fetch.warn": "1s",
		"search.slowlog.threshold.fetch.info": "800ms",
		"search.slowlog.threshold.fetch.debug": "500ms",
		"search.slowlog.threshold.fetch.trace": "200ms"
	}
}'
```
