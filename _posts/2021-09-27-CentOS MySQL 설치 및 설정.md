---
title: CentOS MySQL 설치 및 설정
author: chhak
date: 2021-09-27 00:00:00 +0800
categories: [Linux]
tags: [CentOS, MySQL]
---

1. 설치여부 확인

```
    # yum list mysql*
```

2. 최신버전 MySQL 다운로드 및 설치

```
    - https://dev.mysql.com/downloads/repo/yum/ 접속
    - 아래 작업으로 현재 나의 linux 환경에 맞는 버전 다운로드 및 설치

    # wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
    # yum localinstall mysql80-community-release-el7-3.noarch.rpm
    # yum install mysql-community-server
```

3. MySQL 실행 및 상태 확인

```
    # systemctl start mysqld
    # systemctl status mysqld
```

4. characterset 설정

```
    - 나중에 어차피 하게될 작업을 미리 수행
    # vim /etc/my.cnf

    - 가장 마지막 부분에 다음 내용 추가
    [mysqld]
    ... 중략
    character-set-server=utf8mb4
    collation-server=utf8mb4_unicode_ci
    skip-character-set-client-handshake
```

5. 변경된 설정 적용을 위해 재시작

```
    # systemctl restart mysqld
```

6. root 임시 비밀번호 확인

```
    - 기존 MySQL(5.x) 보다 강력한 보안을 위해 처음 랜덤으로 비번이 설정됨 아래 명령으로 임시 비밀번호를 확인
    - root@localhost: 뒤에 있는 것이 비밀번호

    # cat /var/log/mysqld.log | grep 'temporary password'
```

7. MySQL 초기 보안설정

```
    # mysql_secure_installation

    Enter current password for root (enter for none)? 현재 임시 루트비번 입력
    Set root password? y 입력 후 root 패스워드 설정(2회)
    Remove anonymous users? y 입력 후 익명접근 차단
    Disallow root login remotely? n 입력 후 root 접속 허용
    Remove test database and access to it? y 입력 후 test DB 삭제
    Reload privilege tables now? y 입력 후 현재까지 설정 적용
```

8. MySQL 접속 및 기본 쿼리실습

```
    # mysql -u root -p

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
    mysql> SELECT * FROM `USER`;
```

9. MySQL 외부접속용 root 계정 생성

```
   mysql> create user 'root'@'%' identified by '비밀번호';
   mysql> grant all privileges on *.* to 'root'@'%';
   mysql> flush privileges;
   mysql> exit
```
