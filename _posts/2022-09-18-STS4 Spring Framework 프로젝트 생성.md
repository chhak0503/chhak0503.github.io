---
title: STS4 Spring Framework 프로젝트 생성
author: chhak
date: 2022-09-18 00:00:00 +0800
categories: [Spring]
tags: [Spring]
---

!!!더이상 STS3 플러그인 설치해서 Spring Legacy Project 생성하지 말것(이제 포기 하자)  
!!!STS3 플러그인 공식적으로 지원이 끝나 최신 자바, 이클립스에서 에러발생(못고침)  
!!!STS4 초기 설정(메뉴얼 참고) 끝내고 아래 프로젝트 생성 진행 할 것

---

> 이 방식이 가장 베스트

1. New - Dynamic project 생성
2. project 마우스 오른쪽 클릭 - Configure - convert Maven 프로젝트
   Group Id(패키지명) : kr.co.ch01
   Artifact Id(프로젝트명) : Ch01
3. 프로젝트 마우스 오른클릭 - Spring - Add Spring Project Nature 클릭
4. 프로젝트 마우스 오른클릭 - Properties - Spring - Namespace Support - Enable project specific settings 체크 후 Apple and Close 클릭
5. Spring 컨텍스트 설정파일 생성 및 초기설정

- src - main - resources 폴더 생성
- src - main - resources - application.xml 파일 생성
- spring 홈페이지 - Projects - Spring Framework - LEARN - 최신버전 Reference Doc - Core
  Core - 1.2.1. Configuration Metadata 에서 XML-based configuration metadata 내용 복사&붙여넣기
  application.xml 저장 닫기 후 다시 열면 하단에 Namespaces 탭 생김(Spring 설정파일로 인식된거임)
  6). pom.xml Spring 라이브러리 추가
- Spring IoC/DI 내용 공부할때 spring-context 만 추가 하면 됨
