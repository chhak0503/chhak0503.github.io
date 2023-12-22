---
title: Cloudera 설치
author: chhak
date: 2020-07-21 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

---
[HDFS]  
NameNode - server01  
SecondaryNameNode - server01  
Balancer - server01  
HttpFS - 미설치  
NFS Gateway - 미설치  
DataNode - server02

설정
복제 계수 - 1
HDFS 권한 검사 - 해제
HDFS 블록 크기 - 64  
---
[Cloudera Management Service]  
Service Monitor - server01  
Active Monitor - 미설치  
Host Monitor - server01  
Event Server - server01  
Alert Publisher - server01

---
[YARN]
ResourceManager - server01
JobHistory Server - server01
NodeManager - DataNode(으)로 저장

설정
'Scheduler 클래스' - FifoScheduler 변경
------------------------------------------------------
[Zookeeper]
Server - server02
------------------------------------------------------

[Flume]
Agent - server02

설정
'java heap' - 100
------------------------------------------------------

[HBase]
Master - server02
REST Server - 미설치
Thrift Server - server02
RegionServer - server02

설정
'HBase Thrift Http 서버 설정' - 체크
------------------------------------------------------
[Hive]
Gateway - server02
Hive Metastore Server - server02
WebHCat Server - 미설치
HiveServer2 - server02
------------------------------------------------------
[Oozie]
Oozie Server - server02

설정
'Default Launcher Memory' - 1GB
------------------------------------------------------
[Hue 설치전 python2.7 및 관련 패키지 설치]
#echo "https://vault.centos.org/6.10/os/x86_64/" > /var/cache/yum/x86_64/6/base/mirrorlist.txt
#echo "http://vault.centos.org/6.10/extras/x86_64/" > /var/cache/yum/x86_64/6/extras/mirrorlist.txt
#echo "http://vault.centos.org/6.10/updates/x86_64/" > /var/cache/yum/x86_64/6/updates/mirrorlist.txt
#yum install centos-release-scl


#yum install scl-utils    (centos-sclo-rh baseurl을 찾을 수 없다며 실패 그러면 아래 명령어 실행)
#echo "http://vault.centos.org/6.10/sclo/x86_64/rh" > /var/cache/yum/x86_64/6/centos-sclo-rh/mirrorlist.txt

#yum install scl-utils    (이번에는 centos-sclo-sclo baseurl을 찾을 수 없다며 실패 그러면 아래 명령어 실행)
#echo "http://vault.centos.org/6.10/sclo/x86_64/sclo" > /var/cache/yum/x86_64/6/centos-sclo-sclo/mirrorlist.txt

#yum install scl-utils    (드디어 성공!)

#scl enable python27 bash(해야되나????)

#yum install python27
#source /opt/rh/python27/enable
#python --version

#yum install epel-release
#yum install python-pip
#yum install postgresql-devel
#yum install gcc
#bash -c "source /opt/rh/python27/enable; pip install psycopg2==2.6.2 --ignore-installed"




[Hue] (반드시 Hive, Oozie 설치후 Hue 설치 할 것)
Hue Server - server02
Load Balancer - 미설치

설정
'시간대' - Asia/Seoul
'HBase Thrift 서버' - HBase Thrift Server(server02) 선택
------------------------------------------------------






