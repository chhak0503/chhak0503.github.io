---
title: Spark - MongoDB 실습
author: chhak
date: 2021-07-17 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## 기본 실습

```
$ spark-shell --conf "spark.mongodb.input.uri=mongodb://chhak:1234@192.168.50.82:27017/chhak.member" --packages org.mongodb.spark:mongo-spark-connector_2.11:2.4.0
```

MongoDB 데이터 추출 후 HDFS 파일로 저장

```
scala> import com.mongodb.spark.\_
scala> val memberRDD = MongoSpark.load(sc).map(line => line.toJson)
scala> memberRDD.saveAsTextFile("hdfs:///sample/memberRDD")

scala> val memberDF = spark.read.json("hdfs:///sample/memberRDD/\*")
scala> val userDF = memberDF.select('user, 'name, 'hp, 'pos, 'dep)
scala> userDF.write.format("com.databricks.spark.csv").save("hdfs:///sample/userDF")
```

## Naver Movie 실습

```
$ spark-shell --conf "spark.mongodb.input.uri=mongodb://chhak:1234@192.168.50.82:27017/chhak.movies" --packages org.mongodb.spark:mongo-spark-connector_2.11:2.4.0
```

```
scala> import com.mongodb.spark.\_
scala> val moviesRDD = MongoSpark.load(sc).map(line => line.toJson)
scala> moviesRDD.saveAsTextFile("hdfs:///sample/moviesRDD")

scala> val moviesDF = spark.read.json("hdfs:///sample/moviesRDD/\*")
scala> val movieDF = moviesDF.select('reple, 'score)
scala> movieDF.write.format("com.databricks.spark.csv").save("hdfs:///sample/movieDF")
```
