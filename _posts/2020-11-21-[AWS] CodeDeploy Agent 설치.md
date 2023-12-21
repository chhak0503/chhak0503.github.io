---
title: CodeDeploy Agent 설치
author: chhak
date: 2020-11-21 12:00:00 +0800
categories: [AWS]
tags: [AWS]
---

#### Agent 설치
$ sudo yum update  
$ sudo yum install -y ruby  
$ wget https://aws-codedeploy-ap-northeast-2.s3.ap-northeast-2.amazonaws.com/latest/install  
$ chmod +x ./install  
$ sudo ./install auto


#### Agent 실행 확인
$ sudo service codedeploy-agent start && sudo service codedeploy-agent status

잠시 후... 아래 결과 출력되면 끝  
Starting codedeploy-agent:The AWS CodeDeploy agent is running as PID xxxxx  

Agent 상태 확인할 때 아래 명령어로 하지말것  
systemctl status codedeploy-agent

이걸로 함  
sudo service codedeploy-agent status

아래 메세지 나오면 성공  
The AWS CodeDeploy agent is running as PID xxxxx