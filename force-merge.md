## Force Merge
```
curl -XPOST 'http://localhost:9200/twitter/_forcemerge'
```
- Describle  
给每个shard合并segments,该合并会阻塞所有请求直到合并结束。

- 参数  
 max_num_segments：合并segments数  
only_expunge_deletes：类似于hfile  
flush： force merge后做flush. 默认为true.   

 
