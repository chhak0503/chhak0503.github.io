---
title: Spring MVC 프로젝트 설정
author: chhak
date: 2022-09-18 00:00:00 +0800
categories: [Spring]
tags: [Spring]
---

!!!더이상 STS3 플러그인 설치해서 Spring Legacy Project 생성하지 말것  
!!!STS3 플러그인 공식적으로 지원이 끝나 최신 자바, 이클립스에서 에러발생

1. Spring 프로젝트 생성(Dynamic Web Project로 생성할 것)

2. pom.xml 의존 설정

   - spring-context 라이브러리 추가(spring-context 추가하면 spring-core도 같이 추가됨)
   - spring-webmvc 라이브러리 추가(spring-webmvc 추가하면 spring-web도 같이 추가됨)

3. View 폴더 생성

   - src - main - webapp - WEB-INF - views 폴더 생성

4. 스프링 설정 파일 생성 및 설정

   - src - main - webapp - WEB-INF - resources - application.xml 폴더/파일 생성
   - context:component-scan 선언
   - mvc:annotation-driven 선언(스프링 Web MVC 어노테이션을 위한 태그선언)
   - ViewResolver bean 추가(spring framework - Web Servlet 에서 InternalResourceViewResolver 검색)

5. web.xml 설정작업

   - DispatcherServlet 추가(spring framework - Web Servlet 에서 조금만 내려가면 web.xml 설정 내용 나옴)

6. 컨트롤러, 뷰 생성 및 브라우저 실행
