---
title: MySQL safe모드에서 root 정보 수정
author: chhak
date: 2023-04-27 00:00:00 +0800
categories: [MySQL]
tags: [MySQL]
---

```
서비스 중지
# net stop MySql80

safe모드 실행
# mysqld --datadir="C:\ProgramData\MySQL\MySQL Server 8.0\Data" --console --skip-grant-tables --shared-memory

# 수정(root lock 또는 비밀번호 수정)
select account_locked from user where User='root'
update user set account_locked='N' where user='root';
```
