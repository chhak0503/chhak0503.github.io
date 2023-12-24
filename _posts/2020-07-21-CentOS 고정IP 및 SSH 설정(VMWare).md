---
title: Centos 고정IP 및 SSH 설정(VMWare)
author: chhak
date: 2020-07-21 00:00:00 +0800
categories: [Linux]
tags: [Linux]
---

```
Host System 설정(Windows)
 1. vmnetcfg 파일을 인터넷을 구한다.(https://blogger.pe.kr/560, VMWare Pro버전에 포함, Player버전 미포함)
 2. C:\Program Files (x86)\VMware\VMware Player 에 vmnetcfg 파일 복사
 3. 관리자 권한으로 vmnetcfg 실행 - VMnet8 선택 - Subnet IP 주소 대역 수정
   예) 192.168.111.0 (끝자리 0으로 고정)
 4. NAT Settings - Gateway 확인
   예) 위의 Subnet IP주소 대역을 IP192.168.111.0로 했으면 Gateway 주소는 192.168.111.2 로 설정되어 있음(수정금지)
   참고로 192.168.111.1 은  VMware8 가상 네트워크로 할당됨
 5. Apply - OK

VMware 설정
 1. 가상머신 선택 후 마우스 오른쪽 버튼 - Settings 선택
 2. Network Adapter - Custom: Specific virtual network 에서 VMnet8 (NAT) 선택

Linux System 설정
 1. vi  /etc/sysconfig/network-scripts/ifcfg-ens33vi
   수정 : BOOTPROTO="none"
   추가 : IPADDR="192.168.111.101"
   추가 : NETMASK="255.255.255.0"
   추가 : GATEWAY="192.168.111.2"

 2. systemctl   restart   network
 3. dhclient
 4. ping www.google.com
```
