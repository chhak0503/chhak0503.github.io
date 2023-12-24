---
title: CentOS SSH(Putty) 접속 지연 해결
author: chhak
date: 2021-05-27 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
$ vi /etc/ssh/sshd_config
 84 : GSSAPIAuthentication no <--- no로 수정

$ systemctl restart sshd
$ logout
```
