---
title: Pycharm + GitHub 설정
author: chhak
date: 2020-11-10 00:00:00 +0800
categories: [Git]
tags: [Git]
---

1. github 가입 후 저장소 생성

2. git 설치(Windows 버전)

   - https://git-scm.com/ 다운로드
   - 설치 옵션은 default 진행

3. 설치 완료 후 기본 셋팅

   - Git Bash 실행 > 이름과 메일 주소 입력 (필수)
   - git config --global user.name "이름"
   - git config --global user.email "이메일"

4. Pycharm 셋팅 및 Github 업로드
   - Pycharm 상단 VCS 메뉴 - Enable Version Control Intergration 클릭 - Git 선택 후 OK
   - Pycharm 왼쪽 프로젝트 탐색기 Commit 클릭 - Commit to master 패널에서 Directory 보기 전환
   - Github에 업로드할 프로젝트 디렉터리 체크 선택, 하단 Commit Message 작성 후 Commit 클릭
   - Pycharm 상단 Git 메뉴 - Push 클릭, Define remote 클릭, Github 원격 저장소 주소 붙여넣기, 최종 Push 클릭
