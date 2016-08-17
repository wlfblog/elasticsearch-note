## logstash 安装  
- 下载logstash  
- 解压  

## logstash 使用  
- logstash 配置  
  
```
input {
    file {
        path => "/root/logstashtest/logstash"
        start_position => beginning
        ignore_older => 0
    }
}
filter {
    grok {
        match => { "message" => "%{WORD:id} %{WORD:tag} %{NUMBER:size}" }
    }
}
output {
        elasticsearch {
                hosts => "10.118.31.30:9200"
                document_id => "%{id}"
        }
}
```

## 启动logstash agent  
- logstash agent -f logstash.conf
