### NCP (Overview, Compute/Storage)



##### Overview

##### 클라우드 컴퓨팅 유형

```
Infrastructure Platform
Container Platform
Application Platform
Function Platform
Software Platform

laaS : 서비스로의 인프라를 의미하며 일반적으로 Computing, Networking, Storage 등의 IT리소스를 서비스 형태로 사용합니다.
CaaS : OS 레벨이 아닌 컨테이너 레벨의 기능들을 서비스 형태로 제공합니다
PaaS / aPaaS : 기본 인프라(서버, 네트워크, 스토리지 등)을 직접 관리하지 않으면서 다양한 플랫폼 소프트웨어들을 서비스 형태로 사용합니다.
FaaS : 컴퓨팅 리소스를 서버 단위가 아닌 기능(fuction code) 단위로 실행할 수 있으며, 서버 관리와 구성을 직접 하지 않고도 어플리케이션을 수행할 수 있습니다
SaaS : 완제품 형태로 제공되는 소프트웨어, 어플리케이션, 솔루션을 서비스 형태로 사용합니다.
```



```
Dashboard
- Daily Event, CPU Top5, Security Monitoring-IDS, 상품 이용 내역, 네트워크 이용내역
 결제 정보, 공지 사항, 신규 상품
```



##### 인프라 상품군

```
Compute
- Server 
- SSD Server
- GPU Server
- Virtual Dedicated Server
- Bare-metal
- Auto Scaling
- Cloud Function
- HPC
- Container
- Kubernetes Service

Global
- Global Region
- Global Latency Status : NCP 글로벌 리전 간 글로벌 백본의 속도 상황판

Storage
- Block Storage
- Object Storage : 대량 파일을 저장하는 오브젝트 스토리지
- NAS : 여러 서버가 파일을 공유하는 스토리지
- Backup
- Archieve Storage : 백업, 아카이빙 파일 저장하는 스토리지
- Data Teleporter

Networking
- Load Balancer
- IPsec VPN
- DNS
- NAT Gateway
- Global Internet Service : 국제 인터넷 서비스
- CDN + : 국내 CDN 서비스
- Global CDN : 글로벌 CDN 서비스
- Global Route Manager : DNS 기반의 리전간 로드 밸런싱

Hybrid
- Hybrid Cloud Hosting : 데이터센터 환경과 클라우드 환경을 통합해서 운영할 수 있는 상품
- Vmware on NCP : 엔터프라이즈 기업 고객을 위한 Vmware기반 하이브리드 클라우드 서비스
- Cloud Connect : 온-프레미스 환경과 클라우드를 손쉽게 연결할 수 있는 서비스
```



##### 플랫폼 상품군

```
Database
- MySQL
- MSSQL
- Maria DB
- Cubrid
- PostgreSQL
- Redis
- Tibero
- Cloud DB for MYSQL
- Cloud DB for MSSQL
- Cloud DB for Redis

Analytics
- Cloud Log Analytics
- ELSA
- RUA
- Cloud Hadoop
- Cloud Search
- Data Analytics
- ElasticSearch Service

Media
- VOD Station : VOD 스트리밍 서비스
- Live Transcoder : 동영상 스트림 실시간 변환 서비스
- VOD Transcoder : 동영상 파일을 다양한 화질로 변환
- Image Optimizer : 원본 이미지를 실시간으로 리사이징 변환 및 전송

Game
- Gamepot
```







##### 서비스, 어플리케이션 상품군

```
AI Service
- Clova Face Recongnition : 이미지 속의 얼굴 인식 AI 기능
- Clova Speech Synthesis : 텍스트로 음성 합성 AI 기능
- Clova Speech Recongnition : 음성 인식 AI 기능
- Clova Premium Voice : 고품질 음성 합성 AI 기능
- Papago NMT : AI 기반 번역
- Chatbot : 챗봇 대회 모델 각성과 다양한 메시징 채널 연계
- Papago Korean Name Romanizer : 한국어 로마자 표기법 변환
- Papago NMT : 머신 러닝 기반 번역 AI 기능
- Tensorflow Server : Tensorflow 설치
- Tensorflow Cluster : Tensorflow 분산 환경 처리를 위한 VM 클러스터
- OCR : 인쇄들 상의 문자를 인식 디지털 데이터 자동 추출
- Pose Estimation : 이미지 속 사람을 감지 사람 좌표 정보를 추출
- Object Detection : 객체 위치 감지

Dev Tools
- SourceCommit : 보안 검사 기능이 강화된 Git Repository
- SourceBulid : 빌드 서버 운영이 필요 없는 완전 관리형 병렬 빌드 서비스
- SourceDeploy : 배포 프로세스를 제공하는 자동화 배포 서비스
- SourcePipeline : 리파지토리, 빌드, 배포 프로세스를 통합하여 빠르고 안정적인 S/W 출시를 지원하는 자동화 서비스

Application Service
- API Gateway : API 서비스 등록 관리
- GeoLocation : 사용자 IP에 대한 위치 정보
- Maps : 네이버 지도 API 서비스
- Search Trend : 네이버 검색 트렌드 API 서비스
- Short URL : 단축 URL, API 서비스
- CAPTCHA : 캡차 API 서비스
- SENS : SMS, Push 메시지 전송 서비스
- Simple RabbitMQ : AMQP 기반의 RabbitMQ 클러스터

Biz Application
- Workplace : 워크플로우(결제), 인사, 회계 SaaS
- Workbox : 기업용 파일 공유 서비스
```























##### 관리, 보안 상품군

```
Management
- WMS : 웹사이트 성능 분석 및 상태 모니터링
- Sub Account : 하위 계정 권한 관리
- Monitoring : VM 서버 리소스 모니터링 대시보드, 그래프
- Network Traffic Monitoring : 패킷 정보 수집을 통한 네트워크 트래픽 모니터링
- Cloud Activity Tracer : 사용자의 작업 내용을 로그로 기록하는 상품
- Tools : 네이버클라우드플랫폼과 연동 가능한 다양한 도구
- Resource Manager : 다양한 리소스를 논리적 그룹으로 관리
- Cloud Insight : 클라우드 성능/운영 지표 통합 관리

Security
- ACG : VM 서버들의 IP+포트 기반 접근 제한
- Basic Security : 무료 보안 서비스, Windows 백신, IDS, DDoS 방어
- SSL VPN : 클라우드 네트워크에 접속용 PC agent 방식 SSL VPN
- KMS : 데이터 암호화 키 생성, 관리, 보관
- Security Monitoring : IDS, DDoS 방어, WAF, Linux 백신, IPS 등
- Site Safer : 웹사이트의 악성 코드 포함 여부 진단
- File Safer : 파일의 악성 코드 여부 탐지
- App Safer : 모방리 앱 위변조탐지
- System Security Checker : 서버 보안 설정 상태 점검 및 리포트
- Web Security Checker : 웹 사이트의 취약점 점검 및 리포트
- App Security Checker : 모바일 앱 취약점 점검 및 리포트
- Compliance Guide : 다양한 보안 인증서 및 가이드 문서 제공
```



#### Compute / Storage



##### 전가상화 반가상화

```
전가상화
- 하드웨어 전체를 가상화하는 방식
- 하드웨어를 관리하는 하이퍼바이저(DOM0)가 VM들에게 하드웨어 리소스를 할당하는 방식
- 하이퍼바이저가 모든 리소스를 관리하는 만큼 성능적으로 오버헤드가 발생
- VM은 일반적인 OS 그대로 사용가능

반가상화
- 전가상화의 성능 저하를 해결하고자 모든 명령에 대해 DOM0를 통해 요청하는 방식이 아닌 하이퍼콜을 통해 직접 요청
- 하이퍼콜을 사용하기 위해서는 VM의 OS가 이를 지원해야함
- 하이퍼바이저의 부하를 줄여줌
```









 





##### 서버 특징

```
GPU
- GPU 단위로 할당 - 카드 단위 (GPU Core 단위로 할당하지 않음)
- Pass Through 방식으로 제공
- 최대 2장까지 제공(P40, V100)

Network
- Physical 10Gbps
- Logical 1Gbps
- 실제로 500Mbps ~ 1Gbps 제공(Rx+Tx)
```



##### Server

```
마이크로 서버
- 1vCPU, 1G RAM, 50G HDD
- 지원 OS
CentOS 6.3 6.6 7.2 7.3
Ubuntu 12.04 14.04 16.04
Window 지원 안함

Bare Metal Server
- 기본적인 관리는 IPMI를 통해 관리
- 지원 os
Centos 6.9, 7.4
Oracle Linux 6.9 7.4
Window 2012, 2016

GPU Server
- 제공 os
Centos 7.3 Ubuntu 16.04 Windows Server 2016
```



##### Preinstall Image

```
DBMS
- MS-SQL 2008(std), 2012(std), 2014(std), 2016(exp, std), 2017(exp,std), 2019(std)
```





















##### 서버 Information

```
서버 선택시 제공되는 정보
- 생성일시
- 구동일시
- 스토리지
- Init Script
- Network Interface 적용 가능 여부
- 포트 포워딩 정보
- 반납 보호
- ACG
- SSD 스토리지 추가 여부

유사 서버 생성
- 서버 이미지, 스토리지, 서버 타입, 요금제, Zone, 인증키, ACG 정보를 동일하게 적용
```



##### Private Subnet & Network Interface Operation

```
네이버 클라우드 플랫폼의 서버 네트웍 특징
- 서버에 NIC은 하나가 생성
- IP Alias 허용하지 않음
- 추가 NIC 허용하지 않음

다양한 환경
- VPN으로 연결하는 경우 Peer 네트웍은 대역폭으로 선언되어야 함
- HA 구성이 필요한 경우 VIP가 필요

네이버 클라우드 플랫폼의 방안
- 새로운 NIC를 생성할 수 있게 하되 해당 NIC들만의 네트웍을 구성
- 해당 네트웍은 192.168 대역을 부여

Zone 당 하나의 Private Subnet을 생성할 수 있습니다.
ACG가 적용되지 않음
```























##### Secure Zone

```
금융정보, 개인정보와 같이 격리되어야 하고 모니터링이 되어야 하는 서버를 위치시키기 위한 존

특징
- 인터넷 통신 불가
- 네이버 클라우드 플랫폼 내부의 허용된 서버와의 통신만 가능
- 서버 업데이트 및 어플리케이션 설치도 네이버 클라우드 플랫폼 내부에 허용된 서버를 통해서만 가능
- Secure Zone은 망 방화벽을 통해 Secure Zone 내의 서버를 외부로부터 보호
- 방화벽은 Inbound 뿐만 아니라 Outbound 트래픽까지 제어
- 로그 저장 가능(로그는 CLA에 저장)

호스트 단위 Policy 구성 가능(호스트는 사용자가 보유한 네이버 클라우드 플랫폼의 서버들만 등록 가능)
기본 정책은 ALL Deny
서버 접속을 위해서는 SSL VPN을 이용하거나 Gateway 서버를 구성하여 Gateway 서버를 통해 접속해야함
```



##### disk mount(lvm)

```
fdisk /dev/xvdb
fdisk /dev/xvdd
n p t 8e w

물리볼륨생성
pvcreate /dev/xvdc1
pvcreate /dev/xvdd1

볼륨 그룹 생성
vgreate lvmVG /dev/xvdc1 /dev/xvdd1

논리볼륨 생성 및 포맷
lvcreate --extents 100%FREE -n lvmLV lvmVG
mkfs.ext4 /dev/lvmVG/lvmLV

마운트
mount /dev/lvmVG/lvmLV /lvm
```



##### Public Operation

```
- 공인 IP는 존에 종속
- 공인 IP는 서버에 종속적이지 않으며 공인 IP를 서버에 맵핑하는 구조
```



##### Block Storage

```
- OS의 파일시스템을 기반으로 파일을 계층화하여 저장
- 존에 종속적
```



##### Backup

```
백업 주기
- 1회성
- 1일 1회 전체백업
- 1주 1회 전체백업
- 1주 1회 전체백업 & 매일 1회 증분백업
- 2주 1회 전체백업 
- 2주 1회 전체백업 & 매일 1회 증분백업
- 3주 1회 전체백업
- 4주 1회 전체백업
```



##### Data Teleporter

```
- 어플라이언스를 통한 대용량 데이터의 신속한 이전(1GB, 10GB, 40GB)
- 다양한 네트워크 인터페이스 지원(NFS, FTP, SMB)
```

