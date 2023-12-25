---
title: Tomcat Connection Pool 설정
author: chhak
date: 2020-07-14 00:00:00 +0800
categories: [JSP]
tags: [JSP]
---

```
<!--
	커넥션 풀 설정
	- Tomcat - context.xml 파일에 추가
-->

<Resource
	name="jdbc/java1db"
	auth="Container"
	type="javax.sql.DataSource"
	driverClassName="com.mysql.cj.jdbc.Driver"
	url="jdbc:mysql://127.0.0.1:3306/java1db"
	username="root"
	password="1234"
	maxTotal="8"
	maxIdle="8"
	maxWaitMillis="3000"
	/>

<!-- maxTotal : 풀에 생성되는 최대 커넥션 갯수 -->
<!-- maxIdle : 풀에 유지되어야 할 커넥션 갯수 -->
<!-- minIdle : 최소한으로 유지되어야 할 커넥션 갯수 -->

<!-- 커넥션 풀 설정 -->

<Resource
	name="jdbc/java1_shop"
	auth="Container"
	type="javax.sql.DataSource"
	driverClassName="com.mysql.cj.jdbc.Driver"
	url="jdbc:mysql://127.0.0.1:3306/java1_shop"
	username="root"
	password="1234"
	maxTotal="8"
	maxIdle="8"
	maxWaitMillis="3000"
	/>
<Resource
	name="jdbc/java1_board"
	auth="Container"
	type="javax.sql.DataSource"
	driverClassName="com.mysql.cj.jdbc.Driver"
	url="jdbc:mysql://127.0.0.1:3306/java1_board"
	username="java1_board"
	password="1234"
	maxTotal="8"
	maxIdle="8"
	maxWaitMillis="3000"
	/>
```
