---
title: CentOS vsftp 설치 및 설정
author: chhak
date: 2020-06-01 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
1. vsftp 설치
 $ yum install vsftpd

2. vsftp 설정
 $ vi /etc/vsftpd/vsftpd.conf

    012 : anonymous_enable=NO
    101 : chroot_local_user=YES      (주석해제)
    102 : chroot_list_enable=YES     (주석해제)
    103 : allow_writeable_chroot=YES (새로추가)

3. root 접속허용
 $ vi /etc/vsftpd/ftpusers

    #root      <- 주석

 $ vi /etc/vsftpd/user_list

    #root      <- 주석

 $ vi /etc/vsftpd/chroot_list

	root       <- 추가

4. sftp 사용중지
 $ vi /etc/ssh/sshd_config

    132 : #Subsystem sftp /usr/libexec/openssh/sftp-server  <- 주석

5. vsftp 상태 및 재시작, 부팅 자동실행 등록

 $ systemctl status vsftpd
 $ systemctl restart vsftpd
 $ systemctl enable vsftpd

6. 방화벽 설정/적용
 $ firewall-cmd --permanent --zone=public --add-service=ftp
 $ firewall-cmd --permanent --add-port=21/tcp
 $ firewall-cmd --reload

7. 파일질라 접속 확인
```
