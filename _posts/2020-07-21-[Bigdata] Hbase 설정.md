---
title: Hbase 설정
author: chhak
date: 2020-07-21 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## 환경변수 설정

```
export HBASE_HOME=/home/bigdata/hbase
export PATH=$PATH:$HBASE_HOME/bin
```

## hbase-env.sh

```
// 28라인 주석해제, JAVA 경로 수정
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk

// 89라인 주석해제, HBase 경로 수정
export HBASE_REGIONSERVERS=/home/bigdata/hbase/conf/regionservers

// 126라인 주석해제, Zookeeper 사용여부 true 설정
export HBASE_MANAGES_ZK=true
```

## hbase-site.xml

```
<configuration>
	<property>
		<name>hbase.rootdir</name>
		<value>hdfs://192.168.xxx.101:9000/hbase</value>
	</property>
	<property>
		<name>hbase.master</name>
		<value>192.168.xxx.101:60010</value>
	</property>
	<property>
		<name>hbase.cluster.distributed</name>
		<value>true</value>
	</property>
	<property>
		<name>hbase.zookeeper.quorum</name>
		<value>localhost</value>
	</property>
	<property>
		<name>dfs.replication</name>
		<value>1</value>
	</property>
	<property>
		<name>hbase.zookeeper.property.clientPort</name>
		<value>2181</value>
	</property>
	<property>
		<name>hbase.zookeeper.property.dataDir</name>
		<value>/home/bigdata/hbase-2.x.x/zookeeper_data</value>
	</property>
	<property>
		<name>hbase.unsafe.stream.capability.enforce</name>
		<value>false</value>
	</property>
</configuration>
```
