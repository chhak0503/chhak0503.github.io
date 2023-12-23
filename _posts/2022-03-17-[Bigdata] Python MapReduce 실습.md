---
title: Python MapReduce 실습
author: chhak
date: 2022-03-17 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## 1. hadoop-streaming 라이브러리 복사

```
$ cd ~
$ mkdir MapReduce
$ cp $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-2.10.1.jar /root/MapReduce
```

## 2. mapper, reducer 작성

```
$ cd /root/MapReduce
$ vi word_mapper.py
```

[word_mapper.py]

```
#!/usr/bin/python ← 첫줄에 실행환경 선언
import sys

for line in sys.stdin:
line = line.strip()
words = line.split()

    for word in words:
        print('{}\t{}'.format(word, 1))

:set fileformat=unix ← 반드시 저장하기 전에 fileformat 지정하고 저장닫기
:wq
```

```
$ vi word_reducer.py
```

[word_reducer.py]

```
#!/usr/bin/python ← 첫줄에 실행환경 선언
import sys
word, count = None, 0

for line in sys.stdin:
fields = line.strip().split('\t')

    if fields[0] != word:
        if word is not None:
            print('{}\t{}'.format(word, count))

        word, count = fields[0], 0

    count += 1

print('{}\t{}'.format(word, count))
```

:set fileformat=unix ← 반드시 저장하기 전에 fileformat 지정하고 저장닫기  
:wq

## 3. mapper, reducer 실행권한 부여

```
$ chmod 755 word_mapper.py
$ chmod +x word_reducer.py
```

## 4. 샘플 파일 생성

```
$ vi sample.txt
```

[sample.txt]

```
Deer Bear River
Car Car River
Deer Car Bear
```

:wq

## 5. mapper, reducer 테스트

```
$ cat sample.txt | ./word_mapper.py | sort | ./word_reducer.py
```

## 6. HDFS MapReduce 디렉터리 생성

```
$ hdfs dfs -mkdir /MapReduce
$ hdfs dfs -mkdir /MapReduce/input
$ hdfs dfs -put sample.txt /MapReduce/input
```

## 7. Hadoop MapReduce 실행

```
$ hadoop jar hadoop-streaming-2.10.1.jar \
    -input /MapReduce/input/sample.txt \    ← HDFS 경로
    -output /MapReduce/output \             ← HDFS 경로
    -mapper word_mapper.py \
    -reducer word_reducer.py \
    -file /root/MapReduce/word_mapper.py \  ← 로컬 경로
    -file /root/MapReduce/word_reducer.py   ← 로컬 경로
```
