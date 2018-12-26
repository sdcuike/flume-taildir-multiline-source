# flume-taildir-multiline-source
flume-taildir-multiline-source 解决多行导入问题，java异常堆栈属于多行

#配置：
类型设置类路径com.sdcuike.flume.source.taildir.TaildirMultilineSource
lineStartRegex: 目前处理的是行内包含的关键词，可以包含多个，用"|"隔开
注意：多行合并，请设置flume的默认内存大小

# 例子：
Flume2KafkaAgent.sources.mysource_wf.type= com.sdcuike.flume.source.taildir.TaildirMultilineSource 
Flume2KafkaAgent.sources.mysource_wf.lineContains=ERROR:|WARN:
Flume2KafkaAgent.sources.mysource_wf.channels=mychannel_wf
Flume2KafkaAgent.sources.mysource_wf.filegroups=f2
Flume2KafkaAgent.sources.mysource_wf.filegroups.f2=/data/logs/tester/tester.log.wf

Flume2KafkaAgent.sinks.mysink_wf.channel=mychannel_wf
Flume2KafkaAgent.sinks.mysink_wf.type=org.apache.flume.sink.kafka.KafkaSink  
Flume2KafkaAgent.sinks.mysink_wf.kafka.bootstrap.servers=10.2.39.16:9094
Flume2KafkaAgent.sinks.mysink_wf.kafka.topic=tester.log.wf
Flume2KafkaAgent.sinks.mysink_wf.kafka.batchSize=2
Flume2KafkaAgent.sinks.mysink_wf.kafka.producer.acks=1

Flume2KafkaAgent.channels.mychannel_wf.type=memory  
Flume2KafkaAgent.channels.mychannel_wf.capacity=10000 
Flume2KafkaAgent.channels.mychannel_wf.transactionCapacity=300
conf/flume.conf (END) 



# 建议日志采用json格式输出，对后续处理比较方便
