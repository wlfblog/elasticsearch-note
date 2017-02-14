- 查看集群的分片状态  
```json
http://host:9200/_cat/health?v
epoch      timestamp cluster          status node.total node.data shards  pri relo init unassign pending_tasks max_task_wait_time active_shards_percent 
1487067509 18:18:29  le-elasticsearch green           3         3   1560 1500    0    0        0             0                  -                100.0% 
```

- 查看自定索引的分片状态  
```json
http://host:9200/_cluster/health/video?level=shards
{
cluster_name: "elasticsearch",
status: "green",
timed_out: false,
number_of_nodes: 3,
number_of_data_nodes: 3,
active_primary_shards: 20,
active_shards: 20,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0,
delayed_unassigned_shards: 0,
number_of_pending_tasks: 0,
number_of_in_flight_fetch: 0,
task_max_waiting_in_queue_millis: 0,
active_shards_percent_as_number: 100,
indices: - {
video: - {
status: "green",
number_of_shards: 20,
number_of_replicas: 0,
active_primary_shards: 20,
active_shards: 20,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0,
shards: - {
0: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
1: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
2: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
3: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
4: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
5: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
6: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
7: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
8: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
9: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
10: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
11: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
12: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
13: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
14: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
15: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
16: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
17: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
18: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
},
19: - {
status: "green",
primary_active: true,
active_shards: 1,
relocating_shards: 0,
initializing_shards: 0,
unassigned_shards: 0
}
}
}
}
}
```
