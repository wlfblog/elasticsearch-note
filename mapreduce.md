# mapreduce 入elasticsearch 问题
- elasticsearch version 2.3.5
- hadoop version 2.6.0

## guava包冲突
elasticsearch依赖的guava版本是13 hadoop包是11.

- ，可以修改map-site.xml以下参数
```
<property>
        <name>mapreduce.job.user.classpath.first</name>
        <value>true</value>
</property>
```
- 客户端在提交job时设置
```
Configuration conf = new Configuration();
conf.setBoolean("mapreduce.job.user.classpath.first",true);
```

- 参考链接  
[hadoop文档](http://hadoop.apache.org/docs/current/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduce_Compatibility_Hadoop1_Hadoop2.html)  
