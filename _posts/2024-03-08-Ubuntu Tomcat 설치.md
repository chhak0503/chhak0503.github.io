---
title: Ubuntu Tomcat 설치
author: chhak
date: 2024-03-08 14:33:00 +0800
categories: [Linux]
tags: [Linux, Ubuntu]
---

/*
	Ubuntu Tomcat 수동 설치
	- 2024년 현재 Ubunt 패키지 저장소에는 최신 톰캣 버전 9
	- Java 17, Spring 6.x, Spring Boot 3.x 지원을 위해서는 반드시 Tomcat 10버전으로 설치해야 됨
	- Tomcat 홈페이지에서 직접 Ubuntu용 톰캣 다운로드 함
*/

1. 톰캣 다운로드
 -- 먼저 자바가 설치 되었는지 꼭 확인
 $ java -version

 -- Tomcat 홈페이지 > Tomcat 10.1 > Core - tar.gz 마우스 오른쪽 버튼 > 링크 주소 복사
 $ wget 마우스_오른쪽_버튼으로_다운로드_링크_주소_입력

2. 압축 해제
 $ tar -xvf apache-tomcat-10.x.x.tar.gz

3. /usr/local로 이동 후 심볼릭 링크 생성
 $ mv  apache-tomcat-10.x.x  /usr/local
 $ cd  /usr/local
 $ ln -s   apache-tomcat-10.x.x    tomcat


4. 서비스 등록
 -- 서비스 파일 생성
 $ vi /usr/lib/systemd/system/tomcat.service

 -- 아래 내용 입력 후 저장
-----------------(이거는 입력하는 거 아님)--------------------
[Unit]
Description=tomcat Service
After=network.target syslog.target

[Service]
Type=forking
ExecStart=/usr/local/tomcat/bin/startup.sh start
ExecStop=/usr/local/tomcat/bin/shutdown.sh stop

[Install]
WantedBy=multi-user.target
---------------------(여기까지)-------------------------

5. systemd 재시작
 $ systemctl daemon-reload

6. 톰캣 시작/ 재부팅 등록
 $ systemctl status tomcat
 $ systemctl start tomcat
 $ systemctl enable tomcat

7. 브라우저 접속확인
 - AWS_IP_주소:8080 주소 접속
 - 톰캣 테스트 페이지 출력 확인
 - 참고: AWS는 보안그룹에서 톰캣 포트 8080 인바운드 규칙으로 등록해야 됨
 - 기본적으로 Tomcat 배포 디렉터리는 /usr/local/tomcat/webapps  
 
8. 패키지 파일 생성
 - IntelliJ > Maven > Lifecycle > package 더블클릭(clean 한번하고 package하면 더 좋음)
 - 프로젝트 > target > 프로젝트.war 확인
 
9. 배포
 - 파일질라로 /usr/local/tomcat/webapps에 패키지파일(war) 업로드
 - war Deploy 확인 후 브라우저에서 접속 확인