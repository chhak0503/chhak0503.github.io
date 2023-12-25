---
title: VSCode + GitHub 설정
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

4. vscode 셋팅

   - view > command palette > Git: Initialize Repository 선택 후
   - 바탕화면\workspace\Html 선택
   - view > command palette > Git: Add Remote 선택 후
   - 저장소주소 'https://github.com/chhak/Html.git' 입력
   - remote name에 'origin' 입력

5. 원격저장소 저장하기
   - Source control(3번째 왼쪽사이드 메뉴) 에서 Changes 항목에서 저장소 저장할 파일 +로 Staged 하기
   - 상단에 체크표시로 Commit 하기, Commit 메세지 작성
   - 상단 메뉴버튼에서 최종 Push 하기
   - Github에서 확인하기
