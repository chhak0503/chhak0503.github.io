---
title: Cloudera 최소설치 및 역할 할당 지정
author: chhak
date: 2021-02-17 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

### 최소 설치 구성

- HDFS
- YARN(MR2 Included)
- Zookeeper

### 역할 할당 사용자 지정

[HDFS]

```
NameNode --- cm201
SecondaryNameNode --- cm201
Balancer --- cm201
HttpFS --- 호스트 선택(미설치)
NFS Gateway --- 호스트 선택(미설치)
DataNode --- 모든 호스트
```

[Cloudera Management Service]

```
Service Monitor --- cm201
Activity Monitor --- 호스트 선택(미설치)
Host Monitor --- cm201
Reports Manager --- 호스트 선택(미설치)
Event Server --- cm201
Alert Publisher --- cm201
Telemetry Publisher --- 호스트 선택(미설치)
```

[YARN]

```
ResourceManager --- cm201
JobHistory Server --- cm201
NodeManager --- DataNode
```

[Zookeeper]

```
Server --- cm201
```
