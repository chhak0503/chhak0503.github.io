---
title: hdfs dfs -put ShellScript
author: chhak
date: 2021-09-15 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## move_weather_to_namenode.sh

```
#!/bin/sh
date=$(date +%Y-%m-%d -d '-1days')
echo $date
scp  -r  ./weather/$date root@192.168.56.201:/root/weather/
rm -rf ./weather/$date
exit 0
```

## put_weather_to_hdfs.sh

```
#!/bin/sh
date=$(date +%Y-%m-%d -d '-1days')
hdfs  dfs  -put  ./weather/$date /weather
rm -rf ./weather/$date
exit 0
```
