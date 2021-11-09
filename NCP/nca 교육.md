# NCA 자격증 취득

작성자 : 박성민

작성일 : 202006



### 100. Overview

##### 클라우드의 역사

```
1960년대 가상화라는 용어 사용
- 당시에는 전 가상화 기법을 사용하여 구현
- 애뮬레이터도 존재

다양한 하이퍼바이저의 출현
- IBM의 Logical Partition
   IBM의 유닉스 머신에 사용되는 하이퍼 바이저
- VMWare
- Xen
- Hyper-V
- KVM
```



##### 네이버 클라우드 플랫폼

![1592972476061](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592972476061.png)

##### 공공 클라우드

```
공공 클라우드 인증을 받은 클라우드
- 공공 서비스에 최적화된 공공 서비스 전용 플랫폼 제공
- 공공기관의 엄격한 심의 요건을 충족하고, 다수의 보안 인증을 취득하여 그 안정성을 검증 받음
- 공공 서비스와 물리적으로 분리된 공공 재해복구(DR) 서비스 제공
- 소프트웨어에 대한 철저한 취약점 점검 등 엄격한 기준 통과
- 국내 CC 인증 받은 하드웨어 및 보안 장비 적용
```



##### 금융 클라우드

```
국내 최초의 전문 금융 퍼블릭 클라우드
- 금융 및 핀테크 기업들이 법적인 규제에 대해 안심하고 사용할 수 있는 국내 최초의 전문 금융 퍼블릭 클라우드
- 금융과 핀테크 기업만을 위한 전용 클라우드 데이터 센터
- 국내 금융 컴플라이언스를 완벽하게 충족하는 클라우드 서비스 제공
- 금융 분야에 특화된 체계적인 업무 지원 체계
```



##### Why Cloud?

```
비용 절감
- 데브옵스, 사용한 만큼 지불하는 등 기회 비용 최적화 등을 통한 비용 절감
- 다양한 부가 상품 이용을 통한 개발 비용 절감

빠른 Deploy
- 기존 Legacy 인프라에 비해 빠른 인프라 구성 시간

글로벌 진출시 용이
- 글로벌 리전 활용을 통해 글로벌 진출시 보다 빠르고 손쉬운 인프라 구성

보안
- 인프라에 대한 보안은 클라우드 공급 업체에 위임
- 다양한 보안 상품을 이용하여 보안을 강화
```



##### 네이버 클라우드 플랫폼 구성 요소 - 홈페이지

```
사용하기 쉬운 UX
- 소개
- 상품
- 요금
- 고객지원
- 파트너
- 사용자가이드
- 마이페이지
- 상품별 직관적인 아이콘 구성
```



##### 네이버 클라우드 플랫폼 구성 요소 - 블로그

```
클라우드 관련 기술 자료 제공
- NBP 기술자료
- 활용 TIP 소개
- 신상품 소개
- 고객 사례 소개
- 네이버클라우드플랫폼 이벤트/행사 안내
```



##### 네이버 클라우드 플랫폼 구성 요소 - 유튜브

```
클라우드 관련 기술 자료 제공
- 신규 상품 소개
- 활용법 Webinar
- 고객 사례 소개
```



##### 상품 의존성

```
존 의존 상품
- 서버, CDB와 같이 존에 의존적인 상품

리전 의존 상품
- LB, Object Storage 등 네트웍 및 스토리지와 같이 서비스 지원 상품이 리전에 의존적인 상품

리전 통합 상품
- DNS, Paas, ACG 등과 같이 어플리케이션 상품
```



##### 네이버 플랫폼 서비스 목록

##### Compute

```
Server
비즈니스 환경에 맞춰 원하는 서버를 제공 받을 수 있습니다.

SSD Server
높은 I/O 처리가 가능한 SSD가 장착된 서버를 제공합니다

GPU Server
병렬 처리에 최적화된 GPU 서버의 고성능 컴퓨팅 파워를 제공합니다

Virtual Dedicated Server
고성능의 클라우드 서버를 단독 물리 서버에 제공합니다.

Bare Metal Server
클라우드에서도 가상화 되지 않은 고성능의 물리 서버를 사용할 수 있습니다.

Auto Scaling
사용자가 미리 설정한 이벤트에 따라 서버 수를 자동으로 증가 또는 감소시켜 줍니다

Cloud Functions 
서버 관리에 대한 부담 없이 손쉽게 원하는 비즈니스 로직을 실행할 수 있습니다.

HPC(High Performance Computing)
고급 연산 문제를 해결하기 위한 컴퓨팅 환경을 제공합니다

Container Registry
도커 컨테이너(Docker Container) 이미지를 손쉽게 저장, 관리 및 배포할 수 있습니다.

Kubernetes Service
빠르고 간편하게 Kubernetes 컨테이너를 배포하고 관리할 수 있는 관리형 서비스입니다.
```



##### Storage

```
Object Storage
어떤 종류의 데이터든지 언제 어디서나 데이터를 저장하고 확인할 수 있는 객체 스토리지입니다.

Archive Storage
데이터 아카이빙 및 장기 백업에 최적화된 스토리지 서비스입니다.

File Storage
언제 어디서나 데이터를 저장하고 확인할 수 있는 스토리지 입니다

Block Storage
서버에 할당하여 사용하는 스토리지 입니다

NAS
다수의 서버가 네트워크로 연결해 사용할 수 있는 스토리지 입니다

Backup
백업을 통해 데이터 손실을 최소화할 수 있습니다

Data Teleporter
전용 어플라이언스를 통해 대용량 데이터를 빠르게 이전할 수 있습니다.
```



##### Networking

```
Load Balancer
서버의 성능과 부하량을 고려해 네트워크 트래픽을 다수의 서버로 분산시켜 줍니다

DNS
서비스 운영에 필요한 도메인을 쉽고 간편하게 설정하고 관리할 수 있습니다

Global Internet Service
글로벌 전용 인터넷망을 통해 해외 사용자에게 고품질 서비스를 제공할 수 있습니다.

CDN+
다수의 콘텐츠를 많은 사용자에게 손실 없이 빠르게 전달합니다

Global CDN
세계 어느 곳에서나 빠르고 안정적으로 콘텐츠를 전송할 수 있습니다

IPsec VPN
외부에 있는 고객의 네트워크와 연결하여 서비스를 구성할 수 있습니다.

NAT Gateway
비공인 IP를 가진 다수의 서버를 인터넷 상의 공인 IP를 가진 고객의 호스트와 연결할 수 있습니다.

Global Route Manager
DNS 기반의 다양한 로드밸런싱 방법을 통해 글로벌 네트워크 트래픽을 안정적으로 처리합니다.
```



##### Database

```
Cloud DB for MySQL
MySQL 데이터베이스 서비스를 손쉽게 구축하고 자동으로 관리합니다.

Cloud DB for Redis
Redis 캐시를 클라우드 상에서 간편하게 구축하고 안정적으로 운영합니다.

Cloud DB for MSSQL
MSSQL 데이터베이스를 클라우드 상에서 간편하게 구축하고 안정적으로 운영합니다.

MSSQL
Microsoft가 제공하는 대표적인 관계형 데이터베이스 관리 시스템 (RDBMS)입니다

MySQL
가장 많이 사용하고 있는 오픈 소스 관계형 데이터베이스 관리 시스템 (RDBMS)입니다

CUBRID
대용량 분산 처리에 적합한 오픈 소스 관계형 데이터베이스 관리 시스템 입니다

Redis
고성능 오픈 소스 In memory 데이터 스토어 및 캐시입니다

PostgreSQL
지리 정보 처리와 엔터프라이즈 개발에 최적화된 오픈 소스 관계형 데이터베이스 관리 시스템입니다.

MariaDB
MySQL과 높은 호환성을 유지하는 오픈소스 기반의 데이터베이스 관리 시스템(RDBMS) 입니다.

Tibero
차별화된 아키텍쳐와 다양한 기능이 반영된 DBMS인 Tibero를 Server 설치형으로 제공합니다.
```



##### Security

```
Secure Zone
개인정보 등 중요 정보 자원을 보안이 한층 강화된 별도 Zone에서 관리합니다

Basic Security
모든 고객에게 기본으로 제공되는 무료 보안 서비스입니다

ACG
IP 주소/포트 기반 필터링 기능으로 서버로의 네트워크 접근을 관리합니다

App Safer
모바일 기기에서 앱이 실행될 때 실시간으로 보안 위협을 탐지합니다

Site Safer
회원이 개발한 웹사이트가 해킹 또는 다른 보안문제로 인해 악성코드를 배포하는지 검사하는 서비스 입니다

File Safer
고객의 서비스에서 제공하는 파일과 아웃링크의 악성 여부를 검사할 수 있습니다

Security Monitoring
다양한 보안 위협으로부터 고객의 서비스를 안전하게 보호합니다

SSL VPN
언제 어디에서든지 고객 사이트로 안전하게 접근 가능한 SSL 가상 사설망을 제공합니다

Web Security Checker
고객의 웹 서비스에 대한 주요 취약점을 자동으로 진단합니다

System Security Checker
서버의 운영체제 및 WAS의 보안 설정이 올바르게 되어 있는지 점검합니다. 간단한 설정으로 서버의 보안성을 향상시켜 보세요.

App Security Checker
모바일 앱의 정보 유출 위험을 비롯하여 잠재적인 보안 취약점에 대응할 수 있도록 점검합니다.

Compliance Guide
고객이 보안 인증이나 규제에 대응하는 데 필요한 사항들을 알기 쉽게 정리한 가이드를 제공합니다.

Key Management Service
고객의 중요 정보 암호화에 사용된 키를 고객이 설정한 보안 정책에 따라 엄격히 관리하고 안전하게 보호할 수 있습니다.

Certificate Manager
SSL 인증서의 손쉬운 등록 및 관리 서비스를 제공합니다.
```



##### AI Service

```
Clova Speech Recognition(CSR)
사람의 목소리를 텍스트로 바꿔주어 다양한 음성 인식 서비스에 활용할 수 있습니다

Clova Speech Synthesis(CSS)
입력한 텍스트를 자연스러운 목소리로 재생해주는 음성 합성 API입니다

Clova Face Recognition(CFR)
이미지 속의 얼굴을 감지하고 인식하여 얻은 다양한 정보를 제공합니다

Clova Premium Voice(CPV)
Clova의 인공지능 기술로 더 사람같은, 고품질의 합성음을 제공합니다.

Chatbot
사용자의 질문 의도를 이해하여 고객 대응 등 다양한 서비스에 활용할 수 있는 Chatbot을 손쉽게 만들 수 있습니다.

OCR
인쇄물 상의 글자와 이미지를 디지털 데이터로 자동으로 추출하는 기술입니다.

Papago NMT
입력한 텍스트를 인공신경망 기반 번역 알고리즘을 통해 여러 나라의 언어로 자동 번역해줍니다

Papago Korean Name Romanizer
현행 로마자 표기법에 맞춰 한글 이름을 로마자로 변환해줍니다

TensorFlow Server
대표적인 딥 러닝 프레임워크인 TensorFlow와 머신러닝 패키지들이 설치된 서버(GPU 선택 가능)를 제공합니다.

TensorFlow Cluster
CLI를 사용하여 TensorFlow 분산병렬 처리 환경을 클라우드에서 간편하고 쉽게 구성합니다.

Pose Estimation
이미지 속의 사람을 감지하고 몇명이 어떤 포즈를 취하고 있는지에 대한 좌표 정보를 얻을 수 있습니다.

Object Detection
이미지 내 사람 및 자동차 등 객체의 타입과 위치를 감지하여 정보를 제공합니다.
```



Application Service

```
GeoLocation
고객 서버에서 질의한 IP 주소에 대하여 지역정보 DB를 검색하고 해당 지역의 정보를 고객 서버로 전달합니다

Maps
네이버 지도 기능을 활용해 다양한 위치 기반 서비스를 만들 수 있습니다.

CAPTCHA
이미지를 보여주거나 오디오를 들려주고 정답을 맞추게 하는 방식으로 사람과 컴퓨터를 판별하여 어뷰징을 방지할 수 있습니다

nShortURL
긴 URL을 짧게 줄여주어 글자 수에 제한이 있는 SNS나 SMS를 이용할 때 유용합니다

Simple & Easy Notification Service
서비스에 SMS, PUSH 등을 통한 메시지 알림 기능을 구현할 수 있습니다

API Gateway
안정적인 API 호출을 돕는 다양한 관리 기능과 모니터링 대시보드를 제공합니다.

Search Trend
네이버 통합검색 서비스를 통해 수집되는 검색어 통계를 다양한 기준으로 조회하고 활용할 수 있습니다.

RabbitMQ
메시지 시스템을 구성할 수 있는 AMQP 기반의 오픈소스 메시지 브로커인 RabbitMQ를 VM 설치형으로 제공합니다.

Simple RabbitMQ Service
AMQP 기반의 고가용성 메시지 브로커인 RabbitMQ 클러스터를 손쉽게 배포할 수 있습니다.

Cloud Outbound Mailer
알림, 정보, 마케팅 대량 메일을 UI를 통해서 쉽게 전송하거나 운영하고 있는 서비스에 연결해 전송할 수 있습니다.

Pinpoint
분산 서비스 및 시스템의 성능 분석/진단/추적 플랫폼 서비스인 Pinpoint를 Server 설치형으로 제공합니다.

JEUS
국내 시장 점유율 1위 WAS(Web Application Server) 인 JEUS를 Server 설치형으로 제공합니다.

WebtoB 
국내 대표 차세대 웹서버 WebtoB를 Server 설치형으로 제공합니다.
```



##### Media

```
VOD Transcoder
언제 어디서나 모든 디바이스에서 재생할 수 있도록 미디어 변환 서비스를 제공합니다.

Image Optimizer
원본 이미지를 다양한 해상도의 디바이스에 최적화된 섬네일로 변환하고 배포할 수 있도록 손쉬운 이미지 변환 서비스를 제공합니다.

Live Station
라이브 방송에 필요한 필수 기능을 강력한 인코딩 엔진을 통해 비용 효율적으로 구현할 수 있습니다.

VOD Station
Object Storage에 저장된 MP4 영상 파일을 활용하여 손쉽게 VOD 스트리밍 서비스를 구현할 수 있습니다.
```



##### Management

```
Monitoring
컴퓨팅 자원의 상태를 모니터링하고 이벤트가 발생하면 사용자에게 통보합니다

Sub Account
대표 계정 아래에 서브 계정을 생성해 업무 역할별로 권한 관리를 할 수 있습니다

Web service Monitoring System
고객의 서비스가 제공되고 있는 웹 페이지가 정상적으로 작동하는지 모니터링 합니다

Network Traffic Monitoring
고객 서버에서 발생하는 트래픽을 수집하고 분석하여 정보를 제공 합니다.

Cloud Activity Tracer
Console 및 API 등을 통해 수행되는 계정 활동 기록(접근 기록) 정보를 제공합니다.

Tools
네이버 클라우드 플랫폼과 연동 가능한 다양한 도구를 사용하면 보다 편리하고 효율적으로 관리 및 운영할 수 있습니다.

Resource Manager
네이버 클라우드 플랫폼 내 모든 리소스(Resource)들을 통합적으로 관리할 수 있는 서비스입니다

Cloud Insight
클라우드 환경의 성능/운영 지표를 통합 관리하고, 장애 발생 시 담당자에게 신속히 전달할 수 있는 모니터링 서비스를 제공합니다.
```



##### Analytics

```
Cloud Log Analytics
네이버 클라우드 플랫폼의 여러 서비스에서 발생하는 다양한 로그들을 한 곳에 모아 저장하고 손쉽게 분석할 수 있습니다.

Real User Analytics(RUA)
실제로 웹 사이트에 접속하는 사용자의 성능 정보를 실시간으로 수집하고 분석할 수 있습니다.

Effective Log Search & Analytics
서비스 운영 시 발생하는 애플리케이션 로그를 쉽고 빠르게 저장하고 분석할 수 있습니다

Cloud Hadoop
Apache Hadoop , HBase , Spark , Hive, Presto 등의 오픈소스 기반 완전 관리형 클라우드 분석 서비스입니다.

Cloud Search
홈페이지 내의 검색 기능을 쉽고 빠르게 구현할 수 있습니다.

Elasticsearch Service
Elasticsearch 클러스터를 손쉽게 배포, 운영 및 확장 가능한 서비스입니다.

Data Analytics Service
Data Analytics Service를 이용해 고객과 시장에 대한 이해도를 높일 수 있습니다.
```



##### Dev Tools

```
Jenkins
소프트웨어 개발 시 반복적인 프로세스를 자동화 해주는 Jenkins를 Server와 통합 설치하여 제공합니다.

SourceCommit
개발에 필요한 소스코드와 파일들을 안전하게 저장하고 관리할 수 있는 프라이빗 Git 리파지토리입니다.

SourceBuild
코드 컴파일 및 테스트를 포함한 소스코드 컴파일 그리고 컴포넌트 패키징을 한번에 지원하는 관리형 소스 코드 빌드 서비스입니다.

SourceDeploy
새로 작성되거나 업데이트 된 소스들을 자동으로 서버에 배포하고 적용해주는 자동화 배포 서비스 입니다.

SourcePipeline
리파지토리, 빌드, 배포 프로세스를 통합하여 빠르고 안정적인 소프트웨어 출시를 지원하는 자동화 서비스입니다.
```



##### Business Application

```
WORKPLACE(g)
글로벌 환경에 맞춘 워크플로우 기능이 강화된 기업정보시스템입니다.

WORKPLACE(k)
한국 기업 환경에 맞춘 워크플로우, 인사, 근무, 회계, 비용 기능이 포함된 기업정보시스템입니다.

WORKBOX
스마트하게 협업을 돕는 기업용 파일 공유 서비스입니다.
```



##### Global

```
Global Region
전 세계 주요 거점에 구축한 인프라를 통해 보다 효율적으로 서비스를 구축할 수 있도록 지원합니다

Global Latency Map
네이버 클라우드 플랫폼에서는 전세계 주요 거점(Point of Presence)을 전용회선으로 연결하여 관리하고 있습니다.


```



##### Hybird & Private Cloud

```
Hybrid Cloud Hosting
데이터센터 환경과 클라우드 환경을 통합하여 운영할 수 있습니다.

Cloud Connect
데이터 센터 환경과 네이버 클라우드 플랫폼을 전용 사설 네트워크로 연결할 수 있습니다

VMware on Ncloud
쉽고 빠르게 VMware 기반 클라우드 환경 제공
```



##### IoT

```
Cloud IoT Core
편리한 IoT 디바이스 데이터 수집 및 실시간 처리를 위한 IoT 플랫폼 서비스입니다
```



### 100. Compute / Network

##### Bare Metal Server

```
- 단독으로 사용할 수 있는 고성능 물리 서버를 클라우드 형태로 제공
- 물리 서버에 하이퍼바이저 없이 바로 운영 체제를 설치하여 제공
- 적합한 RAID 구성 방식을 선택할 수 있습니다.(RAID1+0/RAID5)
- 단독 서버를 사용하는 것이기 때문에 성능에 민감한 서비스도 안정적으로 운영 가능
- CentOS, ORACLE Linux와 windows 제공
- 네이버 클라우드 플랫폼의 다양한 서비스와 연계 가능(단, 내서버 이미지, 스냅샷, 추가스토리지 기능 제외)
- 서버 장애시 Live Migration 불가
```



##### 오토 스케일링

```
서버 그룹 모니터링 결과나 사용자가 미리 정한 일정에 따라 가상 서버 수를 자동으로 증가 또는 감소시켜서 수요 변화에 탄력적으로 대응할 수 있게 해 주는 서비스입니다. 고객이 미리 설정한 서비스 모니터링 임계치에 따라서 가상 서버를 자동으로 Scale in/out해 주므로 서비스 수요 변화에 유연하게 대처하고 서비스 가용성을 확보할 수 있습니다.

- 예측하기 어려운 수요에 대한 고가용성 제공
- 시간대별로 트래픽의 변화가 있는 서비스에 대한 효율적인 서버 운용
```



![1592469539691](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592469539691.png)



##### 유형별 이용 시나리오



1. ##### 서버 그룹 모니터링 기반 Auto Scaling

![1592469606700](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592469606700.png)



2. ##### 스케줄링 기반

![1592469631856](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592469631856.png)



3. ##### 메뉴얼

![1592469657891](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592469657891.png)



##### Auto Scaling 관련 용어 정리

```
Scale-in / Scale-out
Auto Scaling Group을 생성하여 고객이 설정한 Policy에 따라 사용하고 있는 가상 서버의 자동 확장(Scale-out) 및 자동 축소(Scale-in)하도록 제공합니다.

Auto Scaling Group
여러 개의 서버 인스턴스들을 Auto Scaling Group 이라는 하나의 그룹으로 묶어 놓게 됩니다.

Launch Configuration
Auto Scaling Group에서 가상 서버를 시작 구성하는 데 사용하는 템플릿입니다. Auto Scaling Group을 생성할 때는 Launch Configuration을 지정해야 합니다

Auto Scaling Group의 최소 용량/최대 용량
Auto Scaling Group의 최소/최대 서버 수를 말합니다. 최소 서버 수의 경우, 항상 이 값과 같거나 이 값보다 더 큰 서버 수가 유지됩니다. 서버를 한 대도 보유하지 않을 수 있게 하려면 0으로 설정합니다.

기대 용량(Desired Capacity)
서버의 수는 기대 용량값에 따라서 조정됩니다. 이 값은 최소 용량 이상, 최대 용량 이하여야 합니다. 이 값이 지정되어 있지 않으면 초기에 최소 용량만큼 서버를 생성합니다.

쿨다운 기본값(초)(Default Cooldown)
새로운 서버가 생성되었다고 해도, Init-Script 실행이나 업데이트 설치 등의 이유로 실제 서비스를 수행할 수 있을 정도로 준비되기까지는 시간이 소요될 수 있습니다. 쿨다운(Cooldown) 시간이란 실제 Scaling이 수행 중이거나 수행 완료된 이후에 모니터링 이벤트 알람이 발생하더라도 무시하도록 설정한 기간입니다.

헬스체크
Auto Scaling Group의 가상 서버에 주기적인 상태 확인을 수행하여 상태가 비정상인 가상 서버를 식별하도록 Health Check를 합니다.

헬스체크 보류 기간
서버가 생성되어 ‘운영중’으로 변경되었더라도 서버의 업데이트 설치 등 작업에 의해서 헬스 체크에 정상 응답하지 못하는 경우가 생길 수 있습니다. 이런 경우 헬스 체크 보류기간을 지정하면 해당 기간 동안에는 헬스 체크에 실패하더라도 서버 헬스에 이상이 있다고 판단하지 않습니다.

헬스체크 유형
서버와 로드밸런서 둘 중에 선택할 수 있습니다. Auto Scaling Group 설정에서 로드밸런서 이름을 지정한 경우에는 헬스 체크 유형 역시 로드밸런서로 설정합니다. 이런 경우 Auto Scaling은 Load Balancer 헬스 체크 방식과 기준에 따라 서버의 상태를 판단합니다.

반납 정책
Auto Scaling 과정에서 추가된 서버에 대한 Scale-in 작업에 대해, 고객이 API 질의 형식으로먼저 반납할 서버를 지정할 수 있습니다. 기본 설정은 먼저 생성된 서버부터 반납합니다.

NAT Gateway
NAT Gateway의 Peer Host를 등록하면, Auto Scaling으로 서버가 생성되면서 해당 Peer Host의 적용 서버에 자동으로 등록됩니다.

Policy
Auto Scaling이 일어나는 방식을 정의하고 있는데, 이를 ‘Policy’로 정의하고 있습니다. Auto Scale-out 이 발생할 때, 몇 대의 가상 서버를 늘릴 것인지, 반대로 Scale-in이 발생할 때 몇 대의 가상서버를 줄일 것인지를 정의합니다. 대수로 정의할 수 도 있고, %로 정의할 수도 있습니다.
```



##### CDN

```
컨텐츠를 Caching 하여 보다 빠르고 안정적으로 사용자에게 전송하는 서비스
- 국내, 국외 주 서비스 지역에 따른 CDN 상품 분리 제공(CDN+ : 국내 GCDN : 국외)
- 원본은 NCP 오브젝트 스토리지 혹은 커스텀 오리진 서버를 둘 수 있음
- 도메인은 랜덤 CDN도메인(*.ntruss.com) 혹은 보유하고 있는 도메인 사용 가능
- 지원 프로토콜은 HTTP/S
```



##### CDN+ 관련 용어 정리

```
서비스 도메인
서비스에서 콘텐츠 전송 시 사용자에게 노출되는 도메인을 의미.
CDN+ 구성 후 이 도메인을 서비스 내에 링크해야 CDN을 통해 콘텐츠를 캐싱하여 전송.

캐싱(Caching)
사용자 요청에 의해 요구되는 콘텐츠를 빠르게 제공하기 위해 캐시 서버에 저장.

원본 서버
캐싱되는 콘텐츠를 가져오기 위한 원본 콘텐츠 저장 서버.

Cache Expiry
CDN에서 캐싱된 콘텐츠가 원본 서버에서 변경되었는지 여부를 확인하는 주기.

HIT
접속자가 요청한 콘텐츠가 유효한 형태로 CDN 캐시 서버에 있어 접속자의 요청에 대해서 바로 응답할 때 'Cache Hit'이라고 함.

MISS
요청한 콘텐츠가 CDN 캐시 서버에 없어서 원본 서버로부터 콘텐츠를 전송받은 후 서버에 저장하는 경우를 'MISS'라고 함. 이전에 요청된 이력이 없거나 유효 시간이 만료된 경우, 요청되었지만 응답한 적이 없거나 캐시를 하지 않도록 설정했을 경우에만 발생.

BYPASS
원본 서버 응답 헤더에 Set-Cookie 헤더가 있거나, Cache-Control 헤더에 private, no-cache, max-age=0 등의 내용이 있는 경우 CDN 서버에서 캐싱하지 않고 접속자에게 전달하는 것을 의미.

Ignore Query String
CDN 서비스가 원본 서버에 요청할 때 '?id=1234'와 같이 URL에 포함된 GET 파라미터를 제거한 후에 요청.

Referrer Domain
콘텐츠가 지정된 도메인에만 제공되게 하여 다른 사이트에서 참조되는 것을 방지. 도메인은 www.domain.com 또는 *.domain.com 형식을 지원하며, 숫자, 영문자, "*", "-", "."만 사용 가능.

Secure Token
QueryString 기반의 Secure Token을 활용하여 허용된 접근에만 콘텐츠를 전달.
```



### 100.Storage/Database



##### Object Storage

```
인터넷상에서 원하는 데이터를 저장하고 사용할 수 있도록 구축된 오브젝트 스토리지
- 객체 기반의 무제한 파일 저장 스토리지
- 콘솔, RESTful API, SDK 등의 다양한 방법으로 오브젝트들을 관리하고, 저장된 파일은 각 파일마다 고유한 접근 URL이 부여되어 인터넷상에서 여러 사용자가 쉽게 접근 가능
- 정적 웹 사이트 호스팅 가능

특징
- S3 Compatibility API 지원
- Data Lifecycle 지원
- Sub Account와의 연동으로 접근 제어 가능
- CDN, Transcoder, Image Optimizer, Cloud Hadoop, Cloud Log Analytics 와 같은 NCP 내 다양한 상품과 통합/연계 지원
```



##### Block Storage

```
간편하게 생성하고 반납하는 효율적인 데이터 저장 공간
- Block Storage는 요청 시 수 분 내에 생성되어 서버에 즉시 연결해 사용할 수 있습니다. 더 이상 사용하지 않을 경우 즉시 반납할 수 있어 비용을 효율적으로 관리할 수 있습니다. 타입은 HDD, SSD로 제공되며 필요한 I/O 성능에 따라 선택할 수 있습니다.
```

##### 상세 기능

![1592879018595](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592879018595.png)





##### Data Teleporter

```
대용량 데이터 이전을 위한 효과적인 솔루션
- 대용량 데이터 (최대 100T) 이전을 위한 전용 어플라이언스 대여 서비스
- 네트워크 비용 절감, 안전하고 빠른 데이터 이관이 가능한 서비스
- 이관 데이터를 NCP Object Storage / NAS에 Import
```



![1592877408740](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592877408740.png)



##### Backup

```
서버 내 파일 및 Preinstall DB에 대한 백업 신청
- 백업 요청서 작성하고 신청하고 서버에 Agent를 설치하면 끝
(ncloud.com -> 고객지원/FAQ -> 자료 -> 백업 요청서)
- 백업수행주기로 8가지 옵션 제공
- 최대 24주까지 백업 파일 보관 가능
```



![1592877645524](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592877645524.png)



| 구분          | 백업 방식                                     |
| ------------- | --------------------------------------------- |
| **파일 백업** | 1회성                                         |
|               | 1일 1회 전체 백업                             |
|               | 1주 1회 전체 백업                             |
|               | 1주 1회 전체 백업 및 매일 1회 증분 백업       |
|               | 2주 1회 전체 백업                             |
|               | 3주 1회 전체 백업                             |
|               | 4주 1회 전체 백업                             |
| **DBMS 백업** | 1회성                                         |
|               | MSSQL 1일 1회 전체 백업                       |
|               | MSSQL 1주 1회 전체 백업                       |
|               | MSSQL 1주 1회 전체 백업 및 매일 1회 증분 백업 |
|               | MYSQL 1일 1회 전체 백업                       |
|               | MYSQL 1주 1회 전체 백업                       |



**서비스 신청정보** 

| **항목**               | **내용**                                                     |
| ---------------------- | ------------------------------------------------------------ |
| 신청항목               | 백업서비스 중 신청하고자 하는 항목 선택<br />1.  신규 백업<br />2. 기존백업 변경<br />3. 기존 백업 삭제 |
| 백업스케줄명           | 백업스케줄을 구분하기 위한 네이밍 기업                       |
| 호스트명               | VM 호스트명                                                  |
| 비공인 IP              | VM의 비공인 IP                                               |
| O/S                    | VM의 OS 및 버전                                              |
| 원본 백업 디렉토리     | 백업이 필요한 디렉토리 or 파일명                             |
| 원본 데이터 사이즈(GB) | 백업이 필요한 원본 데이터의 대략적인 사이즈 정보             |
| 백업수행주기           | 백업수행주기 선택                                            |
| 보관주기               | 백업된 데이터의 보관기간으로 주 단위 기입                    |
| 전체 백업 수행요일     | 전체백업이 수행되는 요일                                     |
| 백업 시작시간(hh:mm)   | 백업수행이 시작되는 시간                                     |
| 소산여부               | 백업된 데이터를 원격의 장소에 이중화 보관<br />1. 신청 2. 미신청 |



##### Cloud DB For Redis

```
자동 복구를 통해 안정적으로 운영되는 완전 관리형 클라우드 인메모리 캐시 서비스
- Redis가 제공하지 않는 자동 Fall-over 기능을 독자적으로 개발하여 제공함으로써 장애발생 시에도 안정적인 서비스를 제공
- 설치 후 Redis와 OS모니터링을 이용할 수 있으며 장애 또는 이벤트 발생 시 사용자의 메일, SMS로 장애 알림
- 네이버 서비스에서 오랜 검증된 Redis 설정을 기본으로 지원
- Redis Cluster 미지원(향후 지원 예정)
```



##### Redis 명령어 제약

```
BGREWIRTEAOF
BGSAVE
SAVE
SLAVEOF
FLUSHALL
FLUSHDB
CONFIG
KEYS
MIGRATE
SHUTDOWN
```



##### 서버 이벤트 유형

| 이벤트명    | 설명                     |
| :---------- | ------------------------ |
| Start       | Redis 서버 시작          |
| Delete      | Redis 서버 삭제          |
| Backup      | 백업 시작, 종료          |
| Replication | 복제 시작, 중단          |
| fail-over   | Redis 서버 failover 관련 |



##### 모니터링 이벤트 유형

| 알람 항목                  | 알람 세부 항목          | 설명                                          |
| -------------------------- | ----------------------- | --------------------------------------------- |
| CPU Utilization            | Used(%)                 | CPU 사용률                                    |
| Swap Usage                 | swap_pct                | swap 메모리 발생량                            |
| Network In/Out             | NetworkBytesIn          | NIC의 초당 inbound byte                       |
| Network In/Out             | NetworkBytesOut         | NIC의 초당 outbount byte                      |
| connected_clients          | connected_clients_count | Redis Server에 접속 중인 클라이언트 연결 수   |
| evicted_keys               | evicted_keys_count      | maxmemory-policy에 의해 발생한 evicted key 수 |
| keyspace_misses            | keyspace_misses_count   | keyspace의 key가 miss된 횟수                  |
| keyspace_hits              | keyspace_hits_count     | keyspace의 key가 hit된 횟수                   |
| master_last_io_seconds_ago | seconds_ago             | 마스터와의 복제 지연 시간                     |
| used_memory                | Used(Kbyte)             | 메모리 사용률                                 |
| instantaneous_ops_per_sec  | second                  | Redis Server에서 처리하는 명령 횟수           |
| node_down                  | boolean                 | node의 다운 여부                              |



### 100. AI / Application

##### 각각의 서비스의 정의를 알고, 제공하지 않는 서비스를 알아야 한다.



##### AI & Application

```
네이버 클라우드 플랫폼 AI
- AI 플랫폼인 Clova, 번역 서비스인 Papago
- 딥러닝을 위한 Tensorflow가 탑재된 서버 이미지 제공(Centos 7.3 Ubuntu 16.04)

네이버클라우드플랫폼 Application
- 네이버에서 사용하는 기수과 서비스를 API로 제공
- Geolocation, Maps, nShortURL, SENS, Search Trend 등 제공
- 네이버 통합검색 서비스를 통해 수집되는 검색어 통계를 다양한 기준으로 조회하고 활용
- 대량 메일 방송을 위한 Outbound Mailer
- 고객 대응에 활용할 수 있는 챗봇
```



##### Geo Location

```
사용자 IP 기반 위치 정보를 제공하는 국내 유일의 서비스
```



##### SENS

```
Simple & Easy Notification Service
서비스에 메시지 및 알람 전송 기능을 간편하게 구현할 수 있습니다. 
메시지 전송 현황을 실시간으로 확인하고, 전송 이력을 특정 기간 별로 조회할 수 있어 효율적인 서비스 운영이 가능합니다.
```



##### Outbound Mailer

```
대량 메일 발송을 위한 메일 발송 상품
- 광고메일 발송을 위한 템플릿 기능, 법적인 기능(제목에 고아고 문구 삽입 및 수신 거부 기능) 제공
- 템플릿에는 네이버 메일과 동일한 입력기인 스마트 에디터를 제공하고 치환 태그 기능을 통해 변수 사용 가능
```



##### 챗봇

```
CS나 주문시스템과 같은 고객 대응을 로봇으로 대체하는 상품
- 학습을 통해 적절한 답변을 자동화, CSR, CSS오 ㅏ연동을 통해 메신저 뿐만 아니라 음성 채팅까지 확장 가능
- 라인, 톡톡, 카카오톡, 페이스북 메신저와 연동
```



##### Clova Speech Recognition(CSR)

```
음성을 텍스트로 변환
- 국내에서 가장 높은 한국어 인식률
- Android 및 iOS SDK 제공
- Rest API 제공
- 한국어, 영어, 일본어, 중국어(간체) 제공
```



##### Clova Speech Synthesis(CSS)

```
텍스트를 음성으로 변환
- 자연스러운 합성음
- 총 9개의 음색 제공(언어별 2개 이하)
- Rest API 제공
- 한국어, 영어, 일어, 중국어, 스페인어 제공
```



##### Clova Premium Voice(CPV)

```
사람의 음성에 가까운 고품질 합성음 제공
```



##### Clova Face Recognition(CFR)

```
입력된 비전 데이터를 통해 얼굴을 인식하고 관련된 다양한 정보를 제공
- 크게 두가지 서비스 제공
 1) 유명인 얼굴 인식
 2) 얼굴 감지
```



##### Clova OCR

```
문서를 인식하고, 사용자가 지정한 영역의 텍스트와 데이터를 정확하게 추출
```

![1592885180863](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592885180863.png)



##### Papago NMT(Neural Machine Translation)

```
통계 기반 번역
입력한 텍스트를 인공신경망 기반 번역 알고리즘을 통해 여러 나라의 언어로 자동 번역
```



##### Pose Estimation

```
이미지내의 주요 신체 영역을 인식하고 해당 영역을 좌표로 변환
- 이미지를 분석하여 신체 영역 좌표를 결과값으로 제공
- RESTful API방식으로 제공
- 이미지는 2MB 이하로 제한
```



##### Object Detection

```
이미지내의 객체를 탐지하고 객체를 분석
- 객체를 탐지하여 객체의 이름, 바운딩 박스, 탐지 정확률을 제공
- RESTful API방식으로 제공
- 이미지는 2MB 이하로 제한
```



##### Search Trend

```
네이버 통합검색 서비스로 조회된 결과에 대한 통계 API
- 특정 키워드의 검색량을 기간별로 확인 가능
- 연령별, 성별, 검색 시 사용한 디바이스별 세분화 조회 가능
- 키워드 및 세분화 조회를 선택하여 REST AIP로 전달하면, 통계 결과를 리턴
- 직관성을 위해 요청된 기간 중 검색 횟수가 가장 높은 시점을 100으로 두고 상대적 비율로 제공
- Applicaton 당 매일 1,000건의 서비스 제공(1,000건 이상은 고객지원 문의)
```



##### nShortURL

```
길고 복잡한 URL을 간단하고 짧게 변경하는 API
```



### 100. Management / Analytics



### 100. Security / Media



##### Live Station

```
실시간 방송을 위한 플랫폼
- 트랜스코딩을 통해 여러 화질로 변환 후, 송풀
- 스트림 상태를 볼 수 있는 모니터링 기능 제공
- Thumbnail Image 추출
- 타임머신(Time Shift)기능으로 놓치지 않는 라이브 방송 서비스 구현 기능
- CDN 연동을 통해 안정적인 송출 가능
```

![1592973329391](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592973329391.png)



##### VOD Station

```
VOD 스트리밍 플랫폼
- Object Storage에 보관된 영상 파일을 이용하여 스트리밍 서비스 제공
- CDN 연동을 통해 안정적인 송출 가능
- Live Station, VOD Transcoder 와 연동하여 사용 가능
- DRM 적용 예정
```

![1592973421536](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592973421536.png)



##### VOD Transcoder

```
고품질 저비용의 클라우드 미디어 파일 변환 서비스
- VOD Transcoder는 미디어 원본 파일을 모바일, PC 등 다양한 디바이스에서 다양한 화질로 시청할 수 있도록 변환해 주는 클라우드 기반의 미디어 서비스
- 시중에서 사용되는 거의 모든 입력 포맷 및 코덱을 지원하여 높은 인코딩 성공률을 보장
- 인터넷 라이브 생중계를 할 수 있는 Live Transcoder, 대용량의 트래픽을 처리할 수 있는 CDN과 결합하여 LIVE/VOD 통합 서비스를 구현 가능
```

![1592973555689](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1592973555689.png)



##### Image Optimizer

```
이미지를 다양한 사이즈로 변환하여 CDN을 통해 제공
- 이미지를 Object Storage에 업로드하면 미리 설정된 툴에 맞추어 이미지 변환
- 이미지는 CDN+ 를 통해 제공
- 리사이즈, 크롭시 자동회전, 얼굴인식 기능 제공
```



##### Workplace

```
- 인사, 회계, 그룹에어 SaaS
- 워크플로우, 인사, 회계시스템에 사내 메신저, 게시판, 조직도 기반 주소록, 메일, 캘린더, 사내 공유 폴더까지 기업에서 필요로 하는 백오피스 시스템을 SaaS로 제공
- 모바일 환경에 최적화 된 App 제공
```





































