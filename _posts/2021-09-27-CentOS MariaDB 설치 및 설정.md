---
title: CentOS MariaDB 설치 및 설정
author: chhak
date: 2021-09-27 00:00:00 +0800
categories: [Linux]
tags: [CentOS, MariaDB]
---

1. MariaDB 설치

```
   $ yum install mariadb mariadb-server
```

2. MariaDB 상태 확인 및 시작

```
   $ systemctl status mariadb
   $ systemctl start mariadb
   $ systemctl enable mariadb
```

3. MariaDB 설정

```
    $ mysql_secure_installation

    Enter current password for root (enter for none)? 엔터
    Set root password? y 입력 후 root 패스워드 설정(2회)
    Remove anonymous users? y 입력 후 익명접근 차단
    Disallow root login remotely? n 입력 후 root 접속 허용
    Remove test database and access to it? y 입력 후 test DB 삭제
    Reload privilege tables now? y 입력 후 현재까지 설정 적용
```

4. MariaDB 접속 및 기본 쿼리

```
    $ mysql -u root -p

    mysql> show databases;
    mysql> create database `mydb`;
    mysql> use `mydb`;
    mysql> show tables;

    mysql> CREATE TABLE `USER` (
    mysql> `uid` VARCHAR(10) PRIMARY KEY,
    mysql> `name` VARCHAR(10),
    mysql> `age` INT,
    mysql> `hp` CHAR(13)
    mysql> );

    mysql> INSERT INTO `USER` VALUES ('a101', '홍길동', 21, '010-1234-1111');
    mysql> SELECT \* FROM `USER`;
```

5. MariaDB 외부접속 root 계정 생성

```
    mysql> create user 'root'@'%' identified by '비밀번호';
    mysql> grant all privileges on *.* to 'root'@'%';
    mysql> flush privileges;
    mysql> exit
```
