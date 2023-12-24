---
title: Centos 고정IP 및 SSH 설정(VirtualBox)
author: chhak
date: 2020-11-26 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
Host System 확인(Windows)
 1. 작업표시줄 오른쪽 하단 네트워크 아이콘 마우스 오른쪽 클릭 - 네크워크 및 인터넷 설정 열기 - 클릭
 2. 네트워크 설정 변경 항목 중 '어댑터 옵션 변경' 클릭
 3. VirtualBox Host-Only Network 마우스 오른쪽 클릭 - 속성 - 인터넷 프로토콜 버전 4(TCP/IPv4) 선택 - 속성 버튼 클릭
 4. 다음 IP 주소 사용 대역확인(손댈거 없음 확인만 함)
예) 기본적으로 VirtualBox는 IP주소 대역을 '192.168.56.1' 서브넷마스크를 '255.255.255.0' 으로 설정됨
 5. 확인 - 닫기

VirtualBox 설정
 1. VirtualBox - 파일 - 호스트 네트워크 관리자 - 선택
 2. 상단 속성아이콘 선택 - VirtualBox Host-Only Network 선택 후 오른쪽 DHCP 서버 사용함 체크해제       
 3. 어댑터 탭의 IPv4 주소, 서브넷 마스크 주소 확인(손댈거 없음 확인만 함)
 4. 닫기 클릭
 5. 가상머신(Server101, Server102, Server103) 각각 마우스 오른버튼 - 속성 - 네트워크 - 어댑터2 탭 클릭 후 호스트 전용 어댑터 선택 - 고급 - 무작위 모드 '모두 허용' 선택 - 확인

Centos 설정
 1. Hostname 설정
  $ vi /etc/hostname

 2. selinux 해제
  $ vi /etc/selinux/config

 3. NetworkManager 서비스 중지
  $ systemctl stop     NetworkManager
  $ systemctl disable  NetworkManager

 4. cd  /etc/sysconfig/network-scripts/
 5. cp ifcfg-enp0s3 ifcfg-enp0s8
 6. vi  ifcfg-enp0s8
   수정 : BOOTPROTO="none"
   수정 : NAME="enp0s8"
   수정 : DEVICE="enp0s8"
   추가 : IPADDR="192.168.56.101"
   추가 : NETMASK="255.255.255.0"

 7. reboot
  재부팅 후 다시 로그인해서
 8. ping www.google.com 확인 후 가상머신에서는 로그아웃
 9. putty 접속 확인
```
