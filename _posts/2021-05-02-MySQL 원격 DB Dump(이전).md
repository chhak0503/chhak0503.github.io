---
title: MySQL 원격 DB Dump(이전)
author: chhak
date: 2021-05-02 00:00:00 +0800
categories: [MySQL]
tags: [MySQL]
---

```
# mysqldump -h 192.168.12.1 -u 아이디 -p패스워드 DB > dump.sql
원격 DB를 로컬 DB에 바로 넣기
로컬 DB에 바로 데이터를 넣는 방법은 위 명령문을 조금 수정하면 됨

# mysqldump -h 192.168.12.1 -u 아이디 -p패스워드 DB | mysql -u 아이디 -p패스워드 DB

// 예시
mysqldump -u krg -p1234 krg | mysql -h 13.209.172.215 -u root -p1234 krg
mysqldump -u lhj  -p1234  lhj  | mysql -h 13.125.27.183  -u root -p1234  lhj
```
