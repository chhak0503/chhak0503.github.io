---
title: CentOS Java 설치(Oracle JDK)
author: chhak
date: 2022-08-11 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
1. 자바 설치확인(먼저 자바가 설치 되었는지 꼭 확인)
 $ java -version

2. 자바 다운로드(오라클 사이트에서 자바 설치 패키지 파일 다운로드)
 $ wget https://download.oracle.com/java/버전/latest/jdk-버전_linux-x64_bin.rpm

3. 자바 설치
 $ yum  localinstall  jdk-버전\_linux-x64_bin.rpm

4. 설치확인
 $ java -version
```
