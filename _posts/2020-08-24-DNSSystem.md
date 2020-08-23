---
title: "Domain Name System"
date: 2020-08-24 06:30:00
categories: network
---
# Domain Name System(DNS)동작 원리 개요
모든 DNS 질의와 응답 메시지는 port 53의 UDP 데이터그램으로 보내짐 <br>
모든 컴퓨터에는 디폴트 DNS 서버의 주소가 등록, 이 디폴트 DNS 서버를 통해서 도메인 이름에 대한 IP주소 정보를 얻게 됨(디폴트 DNS 서버의 주소 알아내는 방법: "$nslookup" 리눅스의 경우 해당 명령어 입력후 server라고 입력)

## 분산 계층 데이터베이스
DNS는 많은 서버를 이용하고 이들을 계층 형태로 구성, 전 세계에 분산시킴. 어떠한 단일 DNS서버도 인터넷에 있는 모든 호스트에 대한 매핑을 갖지 않는 대신 DNS 서버 사이에 분산됨
![dns_layerStructure](https://hankyojeong.github.io/assets/images/dns/dns_layerStructure.png)
- 루트 DNS 서버
  - 인터넷에는 400개 이상의 루트 DNS서버가 있음, 이 루트 네임 서버들은 13개의 다른 기관에서 관리됨.
- 최상위 레벨 도메인(TLD)서버
  - com, org, net, edu 같은 상위 레벨 도메인에 대한 TLD 서버
- 책임 DNS 서버
  - 인터넷에서 접근하기 쉬운 호스트(ex] 웹 서버와 메일 서버)를 가진 모든 기관은 호스트 네임을 IP주소로 매핑하는 공개적인 DNS 레코드를 제공해야 함

ISP들은 로컬 DNS 서버(default DNS 서버)를 갖음, 호스트가 ISP에 연결될 때, 그 ISP는 로컬 DNS 서버로부터 IP주소를 호스트에 제공함

![dns_communicate](https://hankyojeong.github.io/assets/images/dns/dns_communicate.png)
## DNS Caching
DNS는 지연 성능 향상과 네트워크의 DNS 메시지 수를 줄이기 위해 캐싱을 사용, 로컬 메모리에 응답에 대한 정보를 저장함. But, 호스트는 영구적인 것이 아니기 때무네 DNS 서버는 어떤 기간(보통 2일로 설정) 이후에 저장된 정보를 제거함

