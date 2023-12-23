---
title: Hive 실습
author: chhak
date: 2022-03-16 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

http://rocksea.tistory.com/278
http://rocksea.tistory.com/282?category=338297
// 꼭 다운받기
http://vision.ssu.ac.kr/LecData2016-2/grad_system/Hadoop/Hadoop%ED%86%B5%ED%95%A9.pdf

## 기본실습

```
$ hive

hive> SHOW TABLES;
hive> CREATE TABLE member (seq INT, name STRING, hp STRING);
hive> INSERT INTO member VALUES (1, '김유신', '010-1234-1234');
hive> SELECT \* FROM member;
```

## 미국 항공편 운항 통계데이터 테이블 생성

```
CREATE TABLE airline(
    Year INT,
    Month INT,
    DayofMonth INT,
    DayOfWeek INT,
    DepTime INT,
    CRSDepTime INT,
    ArrTime INT,
    CRSArrTime INT,
    UniqueCarrier STRING,
    FlightNum INT,
    TailNum STRING,
    ActualElapsedTime INT,
    CRSElapsedTime INT,
    AirTime INT,
    ArrDelay INT,
    DepDelay INT,
    Origin STRING,
    Dest STRING,
    Distance INT,
    TaxiIn INT,
    TaxiOut INT,
    Cancelled INT,
    CancellationCode STRING,
    Diverted INT,
    CarrierDelay STRING,
    WeatherDelay STRING,
    NASDelay STRING,
    SecurityDelay STRING,
    LateAircraftDelay STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
STORED AS TEXTFILE;
```

### 입력데이터가 HDFS 에 저장되어 있을 경우

```
hive> LOAD DATA INPATH '디렉터리|파일명' OVERWRITE INTO TABLE airline;
hive> LOAD DATA INPATH '/sample/2008.csv' OVERWRITE INTO TABLE airline;
```

### 입력데이터가 로컬(리눅스)에 저장되어 있을 경우

```
hive> LOAD DATA LOCAL INPATH '/home/hadoop/2008.csv ' OVERWRITE INTO TABLE airline;
```

## WordCount 테스트

```
hive> CREATE TABLE obama (text STRING);
hive> LOAD DATA INPATH '/test/obama.txt' OVERWRITE INTO TABLE obama;
hive> SELECT \* FROM obama;
read a book
write a book
Time taken: 0.484 seconds, Fetched: 2 row(s)

hive> CREATE TABLE obama_word_count AS SELECT word, COUNT(1)
hive> FROM (SELECT explode(split(text,' ')) AS word FROM obama) W
hive> GROUP BY word ORDER BY word;
```

### 테이블 export

```
hive> export table obama_word_count to '/backup/WordCountResult';

hive> SELECT \* FROM obama_word_count;
a 2
book 2
read 1
write 1
```

### 하이브 내부 테이블

> 하이브 기본 Warehouse에 저장소에 테이블이 생성되지 않고 location 경로에 지정된 파일, 디렉터리를 데이터로 갖는 테이블

### 하이브 외부 테이블

> 기본 warehouse에 저장소에 테이블이 생성되지 않고 location 경로 디렉터리의 파일들을 데이터로 갖는 테이블(자동으로 INSERT 됨)

## NAVER WORD COUNT 실습

```
CREATE EXTERNAL TABLE naver (
    rank int,
    word string,
    rdate string
)
row format delisemited
fields terminated by ","
location "/sample/naver/naver-20-07-19/" <- 반드시 경로만 지정, 파일 지정 안됨
tblproperties("skip.header.line.count"="1"); <- CSV파일의 첫줄(헤더)을 건너뜀
```

```
hive> SELECT word, SUM(1) as total FROM naver GROUP BY word ORDER BY total DESC;
```

## 연습문제 1

> 데이터베이스 `SALE_2017` 테이블을 SQOOP을 실행해서 HDFS에 IMPORT 하고 HIVE를 실행해서 전체 매출의 합을 구하시오.

```
CREATE TABLE sale_2017 (
    seq INT,
    uid STRING,
    month INT,
    sale INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
STORED AS TEXTFILE;
```

## 연습문제 2

> Weather 외부 테이블 생성하고 평균기온이 가장 높은 순서로 5개 지역 출력

```
CREATE EXTERNAL TABLE `Weather` (
    `c1` STRING,
    `c2` STRING,
    `c3` STRING,
    `c4` TINYINT,
    `c5` TINYINT,
    `c6` FLOAT,
    `c7` FLOAT,
    `c8` FLOAT,
    `c9` FLOAT,
    `c10` FLOAT,
    `c11` TINYINT,
    `c12` STRING,
    `c13` FLOAT,
    `c14` FLOAT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\n'
STORED AS TEXTFILE
LOCATION "/weather/2022-03-08";
```

```
SELECT `c1`, AVG(`c6`) as `avg` from `Weather` GROUP BY `c1` ORDER BY `avg` DESC LIMIT 5;
```
