---
title: CentOS Tomcat 설치 및 설정
author: chhak
date: 2020-07-21 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
1. 톰캣 다운로드
 - 먼저 자바가 설치 되었는지 꼭 확인
 $ java -version

 - 톰캣 공식사이트에서 apache-tomcat-8.x.x.tar.gz  다운로드
 - yum 톰캣 설치는 하지말것(설정 작업 제한)
 - wget 다운로드 주소

2. /root 에서 압축 풀기
 $ tar -zxvf apache-tomcat-8.x.x.tar.gz

3. /usr/local 로 이동 후 심볼릭 링크 생성
 $ mv  apache-tomcat-8.x.x  /usr/local
 $ cd  /usr/local
 $ ln -s   apache-tomcat-8.x.x    tomcat

4. 방화벽 설정(AWS는 제외)
 $ firewall-cmd --permanent --add-port=8080/tcp
 $ firewall-cmd --reload

5. 서비스 등록
 $ vi /usr/lib/systemd/system/tomcat.service

# 아래 내용 입력/저장
[Unit]
Description=tomcat Service
After=network.target syslog.target

[Service]
Type=forking
ExecStart=/usr/local/tomcat/bin/startup.sh start
ExecStop=/usr/local/tomcat/bin/shutdown.sh stop

[Install]
WantedBy=multi-user.target


6. systemd 재시작
 $ systemctl daemon-reload

7. 톰캣 시작/ 재부팅 등록
 $ systemctl status tomcat
 $ systemctl start tomcat
 $ systemctl enable tomcat

8. 브라우저 접속확인
 - 192.168.xxx.xxx:8080 주소 접속
 - 톰캣 테스트 페이지 출력 확인
 - 참고: AWS는 보안그룹에서 톰캣 포트 8080 인바운드 규칙으로 등록해야 됨

9. 톰캣 Document Root 변경
 $ vi /usr/local/tomcat/conf/server.xml

 아래 내용 수정
 152라인 : <Host name="192.168.xxx.xxx" appBase="/home/tomcat/" unpackWARs="true" autoDeploy="true"> <---- 수정
 153라인 : <Context path="" docBase="." reloadable="true"/> <---- 추가

10. 톰캣 unpackWARs 배포권한 755설정
 - 톰캣은 WAR 배포권한이 기본 750이다. 755로 변경해야 한다.
 $ vi /usr/local/tomcat/bin/catalina.sh

 UMASK="0027" 를  "0022" 로 변경(295라인 근처)

11. 톰캣 홈 디렉터리 생성 및 시작페이지 생성
 $ mkdir /home/tomcat
 $ vi /home/tomcat/index.jsp

--------------------- 내 용 ---------------------
<%
out.print("<h3>Hello Tomcat!!!</h3>");
%>

---

12. 톰캣 재시작
 $ systemctl restart tomcat

13. 배포확인
 - 이클립스 - Export - 톰캣 홈 디렉토리 업로드
 - 192.168.xxx.xxx:8080/프로젝트명/xxx.jsp 확인
```
