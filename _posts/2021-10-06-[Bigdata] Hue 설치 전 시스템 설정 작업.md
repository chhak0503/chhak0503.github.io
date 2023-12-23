---
title: Hue 설치 전 시스템 설정 작업
author: chhak
date: 2021-10-06 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

> 아래 명령어를 순차적으로 실행 할 것, 저장소 주소 추가

```
$ echo "https://vault.centos.org/6.10/os/x86_64/" > /var/cache/yum/x86_64/6/base/mirrorlist.txt
$ echo "http://vault.centos.org/6.10/extras/x86_64/" > /var/cache/yum/x86_64/6/extras/mirrorlist.txt
$ echo "http://vault.centos.org/6.10/updates/x86_64/" > /var/cache/yum/x86_64/6/updates/mirrorlist.txt
$ yum install centos-release-scl

$ yum install scl-utils (centos-sclo-rh baseurl을 찾을 수 없다며 실패 그러면 아래 명령어 실행)

$ echo "http://vault.centos.org/6.10/sclo/x86_64/rh" > /var/cache/yum/x86_64/6/centos-sclo-rh/mirrorlist.txt

$ yum install scl-utils (이번에는 centos-sclo-sclo baseurl을 찾을 수 없다며 실패 그러면 아래 명령어 실행)
$ echo "http://vault.centos.org/6.10/sclo/x86_64/sclo" > /var/cache/yum/x86_64/6/centos-sclo-sclo/mirrorlist.txt

$ yum install scl-utils (드디어 성공!!!)
```

### 파이썬2.7 설치

```
$ yum install centos-release-scl
$ yum install scl-utils
$ yum install python27
$ source /opt/rh/python27/enable
$ python --version
```

### psycopg2 패키지 설치

```
$ yum --enablerepo=extras install epel-release
$ yum install python-pip
$ yum install postgresql-devel
$ yum install gcc
$ bash -c "source /opt/rh/python27/enable; pip install psycopg2==2.6.2 --ignore-installed"
```
