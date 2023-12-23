---
title: Spark 실습
author: chhak
date: 2022-03-17 00:00:00 +0800
categories: [Bigdata]
tags: [Bigdata]
---

## Spark 설치

#### Spark 다운로드

```
$ wget http://mirror.apache-kr.org/spark/spark-2.3.2/spark-2.3.2-bin-hadoop2.7.tgz
```

#### 압축해제

```
$ tar zxvf spark-2.3.2-bin-hadoop2.7.tgz
```

#### 링크생성

```
$ ln -s spark-2.3.2-bin-hadoop2.7 spark
```

#### 환경변수 설정

```
$ vi .bashrc
 export SPARK_HOME=/home/hadoop/spark
 export PATH=$PATH:$SPARK_HOME/bin
```

#### 설정적용

```
source .bashrc
```

#### 스파크실행 및 종료

```
spark-shell
:q 또는 Ctrl + D
```

## WordCount 실습

```
scala> var file = sc.textFile("/sample/obama.txt") <- 하둡경로
scala> var word = file.flatMap(\_.split(" "))
scala> var result = word.countByValue()
```

#### 순위, 키워드, 날짜

```
scala> val naverRDD = sc.textFile("/data/naver-20-07-26/\*")
scala> val keywordRDD = naverRDD.map(_.split(",")(1))
scala> val kvRDD = keywordRDD.map((_, 1))
scala> val result = kvRDD.reduceByKey(_+_).sortBy(\_.\_2, false)
scala> print(result.collect.mkString("\n"))
scala> result.saveAsTextFile("/result/naver")
```

#### 단어사전 순서로 정렬

```
scala> sc.parallelize(result.toSeq).sortByKey().saveAsTextFile("/spark_result_key")
```

#### 카운트 오름차순

```
scala> sc.parallelize(result.toSeq).sortBy(\_.\_2).saveAsTextFile("/spark_result_value")
```

#### 카운트 내림차순

```
scala> sc.parallelize(result.toSeq).sortBy(\_.\_2, false).saveAsTextFile("/spark_result_value")
```

#### 단어 카운트

```
scala> var file = sc.textFile('/naver/2018-10-16-\*') <- 하둡경로
scala> var word = file.flatMap(\_.split("\n"))
scala> var result = word.countByValue()
scala> result.foreach(println)

scala> val textFile = sc.textFile("/naver/\*") <- 하둡경로
scala> val counts = textFile.flatMap(line => line.split("\n")).map(word => (word, 1)).reduceByKey((a,b) => a+b)
counts.collect()
scala> var sorted = counts.sortBy(\_.\_2, false)
scala> sorted.saveAsTextFile("/spark_result") // 파일로 저장
```

## Spark csv파일 실습

```
case class Dessert(menuId: String, name: String, price: Int, kcal: Int)

val dessertRDD = sc.textFile("/test/dessert-menu.csv") <- 하둡경로

val dessertDF = dessertRDD.map { record =>
val splitRecord = record.split(",")
val menuId = splitRecord(0)
val name = splitRecord(1)
val price = splitRecord(2).toInt
val kcal = splitRecord(3).toInt
Dessert(menuId, name, price, kcal)
}.toDF

val rowRDD = dessertDF.rdd

val nameAndPriceRDD = rowRDD.map { row =>
val name = row.getString(1)
val price = row.getInt(2)
(name, price)
}

nameAndPriceRDD.collect.foreach(println)

dessertDF.registerTempTable("dessert_table")
val numOver300K = spark.sqlContext.sql("SELECT count(\*) AS num_of_over_300K FROM dessert_table WHERE kcal >= 260")
numOver300K.show
```

## Spark DataFrame

> option 을 적용안하면 기본 컬럼명이 \_c0, \_c1, \_c2 로 지정됨

```
scala> val df = spark.read.option("header", "true").csv("/sample/naver/naver-20-07-24/\*")
scala> val wordDF = df.select(col("제목")) 또는 val wordDF = df.select("\_c1")
scala> val result = wordDF.groupBy("제목").count 또는 val result = wordDF.groupBy("\_c1").count
scala> result.sort(desc("count")).show 또는 result.orderBy($"count".desc).show
```

## Spark Mongodb 연동

```
$ spark-shell --conf "spark.mongodb.input.uri=mongodb://chhak:1234@192.168.100.101:27017/chhak.member" --packages org.mongodb.spark:mongo-spark-connector_2.11:2.4.0
```

```
scala> import com.mongodb.spark.\_
scala> val rdd = MongoSpark.load(sc).map(line => line.toJson)
scala> rdd.saveAsTextFile("hdfs:///user/retheeshs/movies");

scala> val df = spark.read.json("hdfs:///user/retheeshs/movies/\*")
scala> val selectDf = df.select("\_id.$numberLong","movieName").toDF("\_id","movieName")
scala> selectDf.write.mode("overwrite").saveAsTable("mmdb_hdfs_schema.movies")
```

#### mongodb 연동 영화리뷰

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

## WordCloud 시각화를 위한 naver 데이터셋 spark로 가공하기

```
val df = spark.read.csv("/naver/21-01-01/\*")
df.show(15)

df.select("\_c1").show(15)
df.select("\*").where('\_c0 !== "순위").show(13)
val keyword_df = df.select("\_c1").where('\_c0 !== "순위")

keyword_df.count()

#분산파일로 저장
keyword_df.write.save("/result/naver")

#단일파일로 저장
keyword_df.coalesce(1).write.csv("/result/naver4")
```
