# mapreduce 入elasticsearch 问题

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

