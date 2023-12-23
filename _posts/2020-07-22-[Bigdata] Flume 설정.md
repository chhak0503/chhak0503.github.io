---
title: Flume 설정
author: chhak
date: 2020-07-22 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## .bashrc

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
export FLUME_HOME=/home/bigdata/flume
export FLUME_CONF_DIR=/home/bigdata/flume/conf
export PATH=$PATH:$FLUME_HOME/bin
```

## flume-agent1.conf

```
agent1.sources = execGenSrc
agent1.channels = memoryChannel
agent1.sinks = avroSink

agent1.sources.execGenSrc.type = exec
agent1.sources.execGenSrc.command = tail -f /var/log/httpd/access_log
agent1.sources.execGenSrc.batchSize = 10
agent1.sources.execGenSrc.channels = memoryChannel

agent1.sinks.avroSink.type = avro
agent1.sinks.avroSink.hostname = 192.168.xxx.101(Namenode 주소)
agent1.sinks.avroSink.port = 33333
agent1.sinks.avroSink.batch-size = 10
agent1.sinks.avroSink.channel = memoryChannel

agent1.channels.memoryChannel.type = memory
agent1.channels.memoryChannel.capacity = 100000
agent1.channels.memoryChannel.transactionCapacity = 10000
```

## flume-agent2.conf

```
agent2.sources = avroGenSrc
agent2.channels = memoryChannel
agent2.sinks = HDFS

agent2.sources.avroGenSrc.type = avro
agent2.sources.avroGenSrc.bind = 192.168.xxx.101(Namenode 주소)
agent2.sources.avroGenSrc.port = 33333
agent2.sources.avroGenSrc.channels = memoryChannel

agent2.sinks.HDFS.type = HDFS
agent2.sinks.HDFS.hdfs.path = hdfs://192.168.xxx.101:9000/flume/%Y/%m/%d
agent2.sinks.HDFS.hdfs.fileType = DataStream
agent2.sinks.HDFS.hdfs.writeFormat = text
agent2.sinks.HDFS.hdfs.batchSize = 100
agent2.sinks.HDFS.hdfs.rollSize = 0
agent2.sinks.HDFS.hdfs.rollCount = 10000
agent2.sinks.HDFS.hdfs.rollInterval = 600
agent2.sinks.HDFS.hdfs.useLocalTimeStamp = true
agent2.sinks.HDFS.channel = memoryChannel

agent2.channels.memoryChannel.type = memory
agent2.channels.memoryChannel.capacity = 100000
```

## flume-agent1-spooldir.conf

```
agent1.sources = spoolDirSource
agent1.channels = spoolDirChannel
agent1.sinks = avroSink

agent1.sources.spoolDirSource.type = spooldir
agent1.sources.spoolDirSource.channels = spoolDirChannel
agent1.sources.spoolDirSource.spoolDir = /home/bigdata/working/logs
agent1.sources.spoolDirSource.deletePolicy = immediate

agent1.sinks.avroSink.type = avro
agent1.sinks.avroSink.channel = spoolDirChannel
agent1.sinks.avroSink.hostname = 192.168.xxx.101(Namenode 주소)
agent1.sinks.avroSink.port = 4545

agent1.channels.spoolDirChannel.type = memory
agent1.channels.spoolDirChannel.capacity = 100
```

## flume-agent2-spooldir.conf

```
agent2.sources = targetSource
agent2.channels = targetChannel
agent2.sinks = targetSink

agent2.sources.targetSource.type = avro
agent2.sources.targetSource.channels = targetChannel
agent2.sources.targetSource.bind = 192.168.100.101
agent2.sources.targetSource.port = 4545

agent2.sinks.targetSink.type = hdfs
agent2.sinks.targetSink.channel = targetChannel
agent2.sinks.targetSink.callTimeout = 15000
agent2.sinks.targetSink.hdfs.path = hdfs://192.168.100.101:9000/flume/logs/%Y-%m-%d/
agent2.sinks.targetSink.hdfs.fileType = DataStream
agent2.sinks.targetSink.hdfs.writeFormat = Text
agent2.sinks.targetSink.hdfs.useLocalTimeStamp = true
agent2.sinks.targetSink.hdfs.filePrefix = access_log
agent2.sinks.targetSink.hdfs.fileSuffix = .log
agent2.sinks.targetSink.hdfs.threadsPoolSize = 10

agent2.channels.targetChannel.type = memory
agent2.channels.targetChannel.capacity = 100
```
