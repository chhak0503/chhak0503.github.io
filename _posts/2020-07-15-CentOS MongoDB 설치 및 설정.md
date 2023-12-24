---
title: CentOS MongoDB 설치 및 설정
author: chhak
date: 2020-07-15 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
# vi /etc/yum.repos.d/mongodb-org-3.6.repo
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc

# yum install -y mongodb-org

# vi /etc/yum.conf
exclude=mongodb-org.mongodb-org-server, mongodb-org-shell, mongodb-org-mongos, mongodb-org-tools

# vi /etc/mongod.conf
bindIp: 127.0.0.1   -> 0.0.0.0 으로 수정 (외부 접속 허용)

yum 업데이트 시 mongo 자동으로 업데이트 방지
# vi /etc/selinux/config
SELINUX=disabled

# systemctl enable mongod
# systemctl restart mongod

# firewall-cmd --permanent --zone=public --add-port=27017/tcp
# firewall-cmd --reload

# MongoDB 인증
최초 MongoDB를 설치하면 기본 계정은 존재하지 않고 생성해야 한다.
또한 한 계정으로 여러 DB의 권한을 가질 수 없으며 1계정-1DB 원칙이 기존 RDBMS와 다르다.
로컬에서는 계정 정보 없이 mongo 명령만으로 접근이 가능한데 외부에서 접속인증을 통한 원격 접근을 위해서는 계정을 생성해야 한다.

# mongo (최초 접속)

#관리자 계정
> use admin

// 슈퍼관리자
> db.createUser({
    user: "admin",
    pwd: "1234",
    roles: [{role: "root", db: "admin"}]
  })

>exit

#mongo -u admin -p
>use admin

// 일반관리자
> db.createUser({
        user:"chhak",
        pwd:"1234",
        roles:["userAdminAnyDatabase","dbAdminAnyDatabase","readWriteAnyDatabase"]
    })

#사용자 계정
> use test
> db.createUser({
        user:"chhak",
        pwd:"1234",
        roles:["dbAdmin","readWrite"]
    })

> use test
> db.dropUser("chhak")

# vi /ete/mongod.conf
(탭 하면 에러남 반드시 스페이스바로 띄어쓰기)
security:
   authorization: enabled

> mongo test -u chhak -p 1234
```
