---
title: CentOS chrony 설치 및 설정
author: chhak
date: 2021-08-18 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
1. 설치하기
 $ yum install -y chrony

2. 서비스 활성화 및 서비스 기동
 $ systemctl start chronyd
 $ systemctl enable chronyd

3. chrony.conf 환경설정
 $ vi /etc/chrony.conf
    # pool 2.centos.pool.ntp.org iburst     <- 3라인 주석
    server time.bora.net iburst             <- 추가
    server times.postech.ac.kr iburst       <- 추가

4. 서비스 재시작
 $ systemctl restart chronyd

5. 시간 동기화 및 타임존 확인
 $ timedatectl
 --> Time zone: Asia/Seoul 꼭 확인

 만약 다른 값이면
 $ timedatectl set-timezone Asia/Seoul

6. 현재시간 확인
 $ date
```
