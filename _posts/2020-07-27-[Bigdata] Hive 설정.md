---
title: Hive 설정
author: chhak
date: 2020-07-27 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## 환경변수 설정

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
export HIVE_HOME=/home/bigdata/hive
export PATH=$PATH:$HIVE_HOME/bin
```

## hive-site.xml

```
<configuration>
    <property>
        <name>hive.metastore.warehouse.dir</name>
        <value>/hive/warehouse</value>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionURL</name>
        <value>jdbc:mysql://localhost:3306/hive_metastore_db?createDatabaseIfNotExist=true</value>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionDriverName</name>
        <value>com.mysql.jdbc.Driver</value>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionUserName</name>
        <value>hive</value>
    </property>
    <property>
        <name>javax.jdo.option.ConnectionPassword</name>
        <value>1234</value>
    </property>
</configuration>
```
