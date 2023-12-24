---
title: CentOS Crontab 쉘스크립트 실습
author: chhak
date: 2020-05-27 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
#!/bin/sh

today=$(date +%Y-%m-%d)
file="backup-$today.tar.gz"
echo $file

#tar -cvzf /backup/$file /home
```
