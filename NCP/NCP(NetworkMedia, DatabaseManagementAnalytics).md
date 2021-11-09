### NCP(Network/Media, Database/Management/Analytics)



#### Network

##### Network Basic

```
IP 헤더
- TTL : 8bit

CIDR(Classless Inter Domain Routing)
- Classful Addressing
인터넷상의 IP주소를 규격화된 크기로 구분하는 방식

ARP : IP주소에 해당하는 MAC 주소를 얻기 위한 프로토콜
```



| 클래스구분 | 서브넷마스크   | 주소범위                    |
| ---------- | -------------- | --------------------------- |
| A          | 255.0.0.0(/8)  | 0.0.0.0 ~ 127.255.255.255   |
| B          | 255.0.0.0(/16) | 128.0.0.0 ~ 191.255.255.255 |
| C          | 255.0.0.0(/24) | 192.0.0.0 ~ 223.255.255.255 |
| D          | -              | 224.0.0.0 ~ 239.255.255.255 |
| E          | -              | 240.0.0.0 ~ 255.255.255.255 |

##### 

| 포트 | TCP  | UDP  | 설명                                          |
| ---- | ---- | ---- | --------------------------------------------- |
| 20   | TCP  |      | FTP - 데이터 포트                             |
| 21   | TCP  |      | FTP - 제어 포트                               |
| 22   | TCP  |      | SSH                                           |
| 23   | TCP  |      | 텔넷                                          |
| 25   | TCP  |      | SMTP - 이메일 전송                            |
| 53   | TCP  | UDP  | DNS                                           |
| 70   | TCP  |      | 고퍼 프로토콜                                 |
| 80   | TCP  | UDP  | HTTP                                          |
| 88   | TCP  |      | 커베로스 - 인증 에이전트                      |
| 110  | TCP  |      | POP3 - 전자우편                               |
| 111  | TCP  | UDP  | RPC (Remote Procedure Call)                   |
| 123  |      | UDP  | NTP (Network Time Protocol) - 시간 동기화     |
| 139  | TCP  |      | 넷바이오스                                    |
| 143  | TCP  |      | IMAP4 - 이메일 가져오기에 사용                |
| 161  |      | UDP  | SNMP - Agent                                  |
| 162  |      | UDP  | SNMP - Manager 포트                           |
| 179  | TCP  |      | BGP (Border Gateway Protocol)                 |
| 194  | TCP  |      | IRC(Internet Relay Chat)                      |
| 389  | TCP  |      | LDAP  (Lightweight Directory Access Protocol) |
| 443  | TCP  |      | HTTPS                                         |
| 445  | TCP  |      | Microsoft -DS                                 |
| 445  |      | UDP  | Microsoft -DS SMB 파일 공유                   |
| 514  |      | UDP  | syslog 프로토콜 - 시스템 로그 작성            |
| 636  | TCP  |      | SSL 위에 LDAP (암호화된 전송)                 |
| 873  | TCP  |      | rsync 파일 동기화 프로토콜                    |
| 990  | TCP  |      | SSL 위의 FTP (암호화 전송)                    |
| 992  | TCP  |      | SSL 위의 Telnet (암호화 전송)                 |
| 993  | TCP  |      | SSL 위의 IMAP4 (암호화 전송)                  |
| 995  | TCP  |      | SSL 위의 POP3 (암호화 전송)                   |
| 1433 | TCP  |      | MS-SQL                                        |
| 3306 | TCP  |      | MYSQL                                         |
| 3389 | TCP  |      | RDP                                           |



##### VPC(Virtual Private Cloud)

```
클라우드 상에서 논리적으로 격리된 고객 전용 네트워크 공간

상세 기능
- 넉넉한 주소 공간 제공
VPC는 /28 Netmask (16개의 IP) ~ 최대 /16 Netmask (65,536개의 IP)의 네트워크 주소 공간을 제공합니다. RFC1918에 명시된 사설 IP 주소 대역을 이용하실 수 있습니다.
※ 10.0.0.0 - 10.0.255.255 (10.0/16 접두사)
※ 172.16.0.0 - 172.16.255.255 (172.16/16 접두사)
※ 192.168.0.0 - 192.168.255.255 (192.168/16 접두사)

- 다양한 네트워크 토폴로지(Topology) 구성
용도에 따라 네트워크를 세분화하여(서브넷) 고객 맞춤형 네트워크를 구성하실 수 있습니다. 외부 인터넷 접속이 필요한 Front-end용 네트워크는 간단하게 인터넷 게이트웨이와 연결만으로 구성이 가능하며, 또한 안전하게 기업 내부의 데이터를 보관하기 위한 Back-end용 네트워크 공간은 NAT 게이트웨이를 이용하여 외부와의 통신을 최소화하는 형태로 구성하실 수 있습니다. 서브넷에는 /16 ~ /28 네트워크 주소 할당이 가능합니다.

- 네트워크와 서버 자원을 보호하기 위한 NACL과 ACG 제공
VPC의 보안을 강화하기 위해 두 가지 보안 기술을 제공합니다. ① ACG(Access Control Group)은 서버의 Inbound 및 Outbound 트래픽을 제어하고, ② NACL(Network Access Control List)은 Subnet의 Inbound 및 Outbound 트래픽을 제어합니다. 또한 VPC 환경에서는 서버당 총 3개 NIC를 제공되며, ACG는 NIC 단위로 적용이 가능합니다.
```





| 구분           | ACG                                                          | NCAL                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 적용 대상      | 서버의 접근 제어                                             | 서브넷의 접근 제어                                           |
| 지원 규칙      | 허용(Allow)                                                  | 허용 및 거부(Allow/Deny)                                     |
| 상태 저장 여부 | 상태 저장<br/>(규칙에 관계없이 반환 트래픽이 자동으로 허용됨) | 상태 비저장<br/>(반환 트래픽이 규칙에 의해 명시적으로 허용되어야 함) |
| 적용 방법      | ACG를 서버의 NIC에 적용                                      | 서브넷에 있는 모든 서버에 자동 적용됨                        |











#####  Load Balancer

```
LB 구성 방식
- NAT, DR, Proxy

스케줄링 방식
- Round-Robin Scheduling
- Least-Connection
- Source Hash Scheduling
- Weighted Round-Robin Scheduling
- Weighted Least-Connections
- Locality-Based Least-Connetion Scheduling
- Locality-Based Least-Connection Scheduling with Replication Scheduling
- Destination Hash Scheduling

네이버 클라우드 플랫폼 로드밸런서 헬스 체크
- 6초마다 헬스 체크
- 3회 연속으로 OK 혹은 error가 뜨면 바인딩 혹은 언바인딩

접속 정보로 도메인 정보 제공
- 따라서 DNS에는 CNAME으로 등록하여야 함.
- 하지만 Zone apex에 대해서는 RFC1033과 같이 등록 불가

기본적으로 로드밸런서 하나를 생성하면 HAProxy 2개가 생성됨

제약 사항
- 최대 50대 서버를 바인딩 할 수 있음
- 최대 5개의 프로토콜까지 생성 가능
- 한 서버가 여러개의 LB에 바인딩 될 수 있지만 포트별 멀티 바인딩은 지원하지 않음
- 18080 - 18095, 65130, 65131, 64000, 3389, 22 포트는 관리용포트이기때문에 사용 불가

생성 후 변경 가능 옵션
- HTTP Keep-Alive
- connection Idle Timeout
```



##### DNS

```
- 도메인에 대해 IP로 변환하는 서비스
- 입력 가능 항목
 레코드명, 레코드 타입, TTL, 레코드 값
```



| 타입  | 설명                                                         |
| ----- | ------------------------------------------------------------ |
| A     | IPv4 주소를 매칭할 때 사용하는 레코드                        |
| NS    | 도메인의 네임서버 정보                                       |
| AAAA  | IPv6 주소를 매칭하는 레코드                                  |
| CNAME | 해당 도메인 네임의 별칭을 생성하는 레코드                    |
| MX    | preference(우선순위)와 메일을 수신할 서버를 지정하는 레코드  |
| SPF   | 스팸처리 방지                                                |
| PTR   | 역방향 조회 레코드(도메인 네임을 매칭함 주로 ip 주소의 도메인네임 지정에 사용) |
| TXT   | 도메인 설명 레코드(역할 등의 텍스트를 기입하는 용도나 SPF 역할로 사용되는 레코드) |



##### NAT Gateway

```
외부로 나가는 통신의 공인 IP를 지정하는 서비스
- 금융사, 통신사와 같이 나가는 IP에 대한 정보가 필요한 경우 사용
- 일반적으로 서버에 공인 IP를 부여하면 되지만 내부 서버가 다수일 경우 서버마다 공인 IP를 부여하게 되면 관리비용 증가

NAT Gateway를 생성하기 위해 필요한 정보
- NAT Gateway를 통해 통신할 내부 서버
- NAT Gateway 공인 IP
- NAT Gateway와 통신할 외부 IP (Peer IP)
   Peer IP는 대역으로 설정할 수 없음
- Peer향 비공인 IP
```



##### GRM(Global Route Manager)

```
DNS 기반으로 글로벌 트래픽을 안정적으로 로드밸런싱하는 상품
- DNS 기반으로 로드밸런싱
- 글로벌 환경에 지역별 트래픽 분산
- LB와 다른점은 LB가 리전에 국한된다면 GRM은 리전에 국한하지 않고 로드밸런싱
```



| 로드밸런싱타입 | 리소스 타입                                             | Health Check | 설명                                                         |
| -------------- | ------------------------------------------------------- | ------------ | ------------------------------------------------------------ |
| Round Robin    | IP (Server 상품 연계 가능)                              | 설정 가능    | 최대 16개까지 리소스 추가가 가능합니다. 요청에 대해 공평하게 순차적으로 리소스가 응답합니다. |
| Weighted       | IP (Server 상품 연계 가능)                              | 설정 가능    | 최대 16개까지 리소스 추가가 가능합니다. 각 리소스별로 처리하는 트래픽 양에 대한 가중치를 주어 요청에 따른 트래픽을 분배할 수 있습니다. |
| Weighted       | Domain (Load Balancer 상품 연계, 직접 도메인 입력 가능) | 설정 불가능  | 최대 16개까지 리소스 추가가 가능합니다. 각 리소스별로 처리하는 트래픽 양에 대한 가중치를 주어 요청에 따른 트래픽을 분배할 수 있습니다. |
| GeoLocation    | Domain (Load Balancer 상품 연계, 직접 도메인 입력 가능) | 설정 불가능  | 글로벌 서비스에 최적화된 로드밸런싱 타입입니다. 사용자의 위치를 기준으로 대륙 혹은 국가 단위 분기가 가능하며, IP 대역을 기준으로 한 분기 설정도 가능합니다. Geo Map 메뉴를 통해 고객에게 꼭 맞는 Map을 손쉽게 구성할 수 있으며, IP 대역 기준으로 CIDR Map을 구성하는 것도 가능합니다. |



##### CDN +

```
사용자에게 컨텐츠를 보다 빠르고 안정적으로 전송하는 서비스
 - 원본 위치는 파일 스토리지 혹은 오리진 서버를 들 수 있음
 - CDN을 사용하기 위해서는 CDN 도메인 혹은 보유 도메인을 이용하여야 함
```



##### CDN 옵션

```
Purge
- CDN 캐시서버에 저장 되어 있는 콘텐츠를 삭제하는 기능

Cache expriy
- CDN에서 캐싱된 콘텐츠가 원본서버에서 변경되었는지 여부를 확인하는 주기를 지정

Streaming
- 네트워크를 기반으로 사용자들에게 멀티미디어 정보를 실시간으로 제공하는 기술

Secure token
- 토큰 기반의 인증으로 허용된 접근에만 콘텐츠를 전달

Ingnore query string
- CDN 서비스가 원본 서버에 요청할 때 ?id=1234 와 같이 URL에 포함된 GET 파라미터를 제거한 후에 요청

Referrer domain
- 콘텐츠가 지정된 도메인에만 제공되므로 다른 사이트에서 참조되는 것을 방지함

Access log
- CDN 사용 로그를 확인할 수 있는 기능 
- Object Storage에 저장

HIT
- 접속자가 요청한 콘텐츠가 유효한 형태로, CDN 캐시 서버에 있어 접속자의 요청에 대해서 바로 응답할 때 'HIT' 이라고 함

MISS
- 요청한 콘텐츠가 CDN 캐시서버에 없을 경우 원본서버로부터 콘텐츠를 전송 받은 후 서버에 저장하게 되는 경우를 'MISS'라고 함

BYPASS
- 원본서버 응답 헤더에 Set-Cookie 헤더가 있거나 Cache-Control 헤더에 private, no-cache, max-age=0 등의 내용이 있는 경우 CDN 서버에서 캐싱하지 않고 접속자에게 전달하는 것을 의미함

동적 콘텐츠
- PHP/ASP/JSP 등을 이용하여 접속자 별 요청에 대해서 서로 다른 콘텐츠를 응답하는 경우

정적 콘텐츠
- 일반적으로 JPG,PNG,GIF,MP4,ZIP,PDF 와 같이 모든 접속자에게 동일한 콘텐츠를 전달하는 경우
```



#### Database

##### Cloud DB for Mysql

```
최대 32 vCPU, 256GB메모리 6TB DISK까지 확장가능

DB 엔진 버전
- Mysql 5.7.19
- Mysql 5.7.25
- Mysql 5.7.29
- Mysql 8.0.18
Cloud DB ofr Mysql은 Standard 타입과 High-memory 타입으로 제공
최대 5대의 Slave DB 추가 가능
데이터 스토리지 HDD, SSD 중 선택 가능
- 기본 10GB부터 10GB 단위로 최대 6000GB까지 자동 증가
고 가용성이 지원되는 스펙과 Stand alone 형태로 생성 가능
Secure zone에 생성 가능
- Secure zone에 생성된 서버는 Public domain을 제공하지 않음
Public domain 부여를 통해 외부에서 접근가능
```







##### CDB Operation

```
1. DB Processlist 확인
제공 항목 : Session ID, USER, HOST(IP), DB, Command, Time, State
2. Slave DB Replication 확인
3. DB 서버 로그 확인
4. DB 백업 설정 및 복원
- 백업은 하루에 한번 매일 수행되며, 사용자 설정에 따라 최대 30일까지 보관이 가능
- 관련 정보 : DB서비스 이름, Backup보관일, Backup시작 시간, Backup 데이터 크기, 마지막 Backup일자, 상세정보보기
- 백업 파일로 복원 시, 신규 VM이 생성되며 이 때 데이터베이스 서버는 Recovery 모드로 복원되며 데이터 조회만 가능합니다.
5. DB 엔진 업그레이드
- Mysql의 Minor 버전 Rolling 업그레이드 지원
- 버전 업그레이드는 동일한 서비스 내 모든 DB 서버 버전이 변경
- Master DB는 Standby Master DB로 전환하여 서비스 접근 차단을 최소화
- 업그레이드 작업은 1대씩 순차적으로 진행
```



##### 이벤트 설정

##### OS 영역 이벤트 항목

| 알림 항목    | 알림 세부 항목           | 설명                     |
| ------------ | ------------------------ | ------------------------ |
| CPU          | Used(%)                  | CPU 사용량               |
| CPU          | lowait(%)                | CPU lowait 사용량        |
| Memory       | used(%)                  | 메모리 사용량            |
| Swap         | swap_pct                 | Swap 메모리 발생량       |
| Disk I/O     | Read bytes / Write bytes | Disk의 읽기/쓰기 발생량  |
| Network      | bps in                   | NIC의 초당 outbound byte |
| Load Average | 1 min/ 5 min/ 15 min     | 서버 부하량              |
| Filesystem   | used (%)                 | 디스크 사용량            |



##### DB 영역 이벤트 항목

| 알림 항목   | 알림 세부 항목 | 설명                        |
| ----------- | -------------- | --------------------------- |
| Connetions  | Running        | DB 접속 세션 수             |
| SlowQuery   | SlowQueryCount | 1초 이상 실행되는 쿼리 개수 |
| Replication | Stop           | 복제 중단 정보              |
| Replication | Delay          | 마스터 대비 복제 지연 시간  |
| DB          | Down           | DB 다운 정보                |



##### Cloud DB for MSSQL

```
최대 24 vCPU, 128GB 메모리 지원, 2TB까지 Disk 확장가능
standard : 최대 vCPU 16, 32GB 메모리
High-memory : vCPU 24, 128GB 메모리
생성 시 고가용성 지원을 클릭하면 Principal DB와 Mirror DB가 생성되며 2개의 DB에 대한 요금이 발생합니다.

- 고가용성이 지원되는 타입과 Stand-alone 타입 선택 가능
 Stand-alone 타입으로 생성하였다가 고가용성 지원 타입으로 변경 가능
- 1분 단위의 쿼리 레벨 성능 분석 제공
- 자동 Fail-over 지원
- Slave DB는 5대까지 추가 가능

mysql, mssql 차이
- mysql 10G 시작 10G 단위로 크기증가 6TB까지 증가
- mssql 100G 시작 2TB까지 증가
```



##### CDB Operation

```
1. DB Config 및 Config Group 관리
- DB Config 관리를 클릭하면, 선택한 DB 서버에 적용할 Config Group을 변경할 수 있습니다.
- 서비서 특성에 맞게 sp_config와 trace flag를 변경해 config group을 생성할 수 있음
- Config group 생성 뿐만 아니라 변경, 삭제 가능
- Config group이 적용도니 서버가 있을 경우, config group 삭제 불가능
- Config group을 이미 적용한 Cloud DB 서비스가 있다면, 해당 DB서버들도 변경 적용
(재시작이 필요한 경우, 서버 재시작후 적용)

2. Slave DB
- log shipping 방식으로 생성되며, transaction log 백업을 restore하는 동안에는 읽기가 불가능하여 일반 서비스 용도로는 사용이 불가
- 매일 주기적인 BI 및 Batch 작업에 적합함
- 시간 단위로 읽기 가능한 시간을 최대 20시간까지 설정 가능
- 읽기 가능 Slave는 최대 5대까지 생성 가능
- 읽기 가능 Slave의 spec을 변경하면, principal 과 mirror 서버도 함께 변경

3. Operation 쿼리 분석
- 쿼리 수행 횟수 대비 CPU 소모량과 메모리 읽기 수는 상관관계 및 분포를 버블 차트로 표현
- X축은 해당 쿼리의 일별 수행 횟수 합계
- Y축은 해당 쿼리의 일별 CPU 소모량의 합계ㅒ
- 버블의 크기로 해당 쿼리의 메모리 읽기 수 확인
사이즈가 클수록 메모리,CPU가 크다
```















##### Cloud DB for Redis

```
생성 시, 고가용성 혹은 Stand alone 스펙 여부 선택가능
Cloud DB For Redis 생성 전 사전 준비 사항
- Cloud DB for Redis는 현재 네이버클라우드플랫폼 내부에서만 접근이 가능
- Redis캐시는 인메모리 캐시로 캐시에 저장될 데이터의 사이즈를 예측하는 것이 중요함
Stand-alone과 고가용성 스펙 모두 자동 백업 선택 가능(최대 7일)
Secure zone 내 생성 가능
Standard 타입과 High-memory 타입 중 선택 가능
```



##### Cloud DB for Reid Operation

```
1. Config 관리
- Hash-max-ziplist-entries, hash-max-ziplist-value 등 7개의 항목에 대해서 변경이 가능

2. monitoring 설정
- Redis서버에 대한 Redis Dashboard와 OS Dashboard를 제공합니다
- 최근 4주 이내의 모니터링 지표를 확인 할 수 있음

3. Back-up 설정
- 백업 파일은 별도의 데이터 스토리지에 저장
```



##### Management

```
IT 인프라와 서비스를 실시간으로 모니터링하고 관리하여 고객에게 24시간 365일 안정적인 클라우드 서비스를 제공하는 서비스며 Monitoring, Sub account, WMS, Network Traffic Monitoring, Cloud Activity Tracer, Tools, Resource Manager, Cloud Insight가 제공
```



##### Sub Account

```
RBAC(Role-Based Access Control) 기능을 통한 권한 관리

Dashboard
서브 계정이 접속할 수 있는 페이지 설정 및 서브 계정 수 / 그룹 수 / 정책 수 / 접속 페이지 설정 / 최근 이벤트 로그를 확인 할 수 있다.

Sub Accounts
새로운 서브 계정을 생성하거나 기존에 있는 서브 계정의 정보를 수정/삭제, 일시정지/해지 가능
각 서브 계정 상세 페이지에는 그룹, 정책을 추가/삭제하거나 API Gateway사용에 필요한 API Key를 관리하고 이벤트 로그를 확인 할 수 있다.

Groups
서브 계정 그룹을 생성/삭제하거나 이름을 변경할 수 있습니다.
그룹에 서브 계정이나 정책을 추가/삭제하여 다수의 서브 계정들에 동일한 정책이 반영되도록 할 수 있습니다.

Policies
서브 계정이 이용할 수 있는 권한들을 묶어 정책으로 제공합니다. 정책 목록 및 정책의 유형, 권한, 적용대상을 확인 할 수 있습니다.
```



##### WMS(Web service Monitoring System)

```
WMS 모니터링 유형
- Virtual 테스트 : 서버에서 가상 브라우저를 생성하여 웹사이트의 품질 테스트 진행
- Scenario 테스트 : 실제 사용자 입장에서 로그인부터 이동 경로에 따른 웹사이트의 정상 동작여부 파악
- Real Browser 테스트 : Chrome, Firefox, Internet Explorer 기반의 테스트 수행

WMS Monitoring 결과
1. Load time
2. Service Health : 최근 측정한 데이터를 기반으로 서비스 종합 상태를 등급으로 나타냅니다.
3. Today Event : 현재 테스트 중인 URL에서 금일 발생한 이벤트 수를 보여줍니다.
4. Scenario : 테스트시나리오 내용을 보여줍니다.
5. File Request : 다운로드 한 구성 요소들의 목록을 보여줍니다.

Error Log : 이벤트 발생 내역에 대한 상세 내용을 보여줍니다.
Water Fall : 서비스를 구성하는 컨텐츠들의 Network 상세 정보를 Waterfall로 확인할 수 있습니다.
```



##### Network Traffic Monitoring

```
패킷 정보를 분석하여 다양한 트래픽 정보 모니터링

기본으로 제공되는 7개 Default Chart
- Region별 Internet Outbound
- Region별 전용회선 Outbound
- 서버별 Internet
- 서버별 전용회선
- 서버 그룹별 Internet
- 서버 그룹별 전용회선
- 국가별 Internet

차트 공통 기능
- Traffic/Flow/Packet 중 측정 단위 선택
- 기간 선택 : 모니터링 가능 기간 내에서 날짜 선택
- Top(Max30) : Top에 지정한 수 이하의 정보가 내림차순으로 출력
- Line, Area, Stack으로 그래프 형태를 선택할 수 있다.
```















##### Cloud Activity Tracer

```
- Console 및 API를 활용한 계정 활동과 Auto Scaling 등의 자동 스케줄러를 이용한 작업 활동을 포함하여 현재 약 155개 종류의 네이버 클라우드 플랫폼 계정 활동 로그를 자동으로 수집하고 기록
- 생성된 계정 활동 로그는 CLA와 연동되어 저장

상세 기능
- 기간 검색 옵션을 통해 검색이 가능하며 조회 가능 데이터는 최근 30일 이내의 데이터에 한합니다
- 작업 내역/ 계정명(root, sub account) / 요청지 IP / 관련 서비스 /리전 /작업 상태에 대해서 검색이 가능
- 약 155 종류의 네이버클라우드플랫폼 계정 활동에 대한 내역 수집이 가능

최대 100GB의 데이터를 30일간 보관합니다.
Cloud Activity Tracer의 로그는 CLA에 저장되며 CLA에 저장된 데이터에서 검색한 결과를 엑셀파일로 다운로드 할 수 있습니다. 다만 전체 데이터가 아닌 검색결과의 화면에 보이는 내용만 다운로드가 가능
```



##### Cloud Insight

```
클라우드 환경의 가시성/통찰력을 확보, 서비스의 연속성을 향상
Planned Maintence -> 발송 x
```



#### Analytics

```
데이터를 효과적으로 수집하고 통합 분석하는 서비스

CLA(Cloud Log Analytics)
- 네이버클라우드플랫폼 인프라 상에서 발생하는 다양한 로그들을 한곳에 모아 저장 및 분석
RUA(Real User Analytics)
- 웹 사이트에 접속하는 사용자의 성능 정보를 실시간으로 수집 및 분석
ELSA(Effective Log Search and Analytics)
- 애플리케이션 로그를 쉽고 빠르게 저장 및 분석
Cloud Hadoop(빅 데이터 분석)
- Apache Hadoop, Hbase, Spark, Hive 등의 오픈 소스 기반 완전 관리형 클라우드 분석 서비스
Cloud Search
- 클라우드 기반으로 검색 서비스 구현
Elasticsearch Service
- Elasticsearch 클러스터를 손쉽게 배포, 보호, 운영 및 확장하는 관리형 서비스
Data Analytics Service
- 웹 사이트를 방문하는 고객의 행동 데이터를 분석 및 시각적 데이터 제공
```













##### CLA(Cloud Log Analytics)

```
서버에서 발생하는 모든 텍스트형태의 로그를 수집할 수 있다.

쉬운 에이전트 설치 및 실행
- CLA는 네이버클라우드플랫폼에서 제공하는 에이전트를 설치하면 바로 사용할 수 있다.

손쉬운 데이터 다운로드
- 필요한 데이터는 엑셀 등의 형식으로 대시보드에서 바로 다운가능
- 로그 검색 결과를 보유하고 있는 Object Storage에 저장 가능

```



##### RUA(Real User Analytics)

```
실제로 웹사이트에 접속하는 End-User단에서의 체감 성능 정보를 수집할 수 있습니다.
```



##### ELSA(Effective Log Search and Analytics)

```
애플리케이션 로그를 쉽게 저장하고 분석할 수 있는 서비스
- 직관적인 대시 보드 제공
- 모바일 크래시 로그 분석 기능 제공
ELSA 모바일 SDK를 사용하여 앱 크러쉬 정보를 저장하고 분석할 수 있습니다.

상세기능
Integrated Log Search Board
- 다양한 Widget 기능을 통해 저장된 애플리케이션 로그 정보를 하나의 Dashboard에서 확인할 수 있습니다.
- Dashboard에서 확인되는 정보는 실시간으로 발생되는 데이터를 Aggregate하여 보여줍니다.

Log Search
- MC화면의 Log Search에서는 기본값으로 현재 시간 기준으로 24시간 동안 발생한 로그에 대한 시간대별 로그 수집 개수 그래프와 상세 로그 형태로 제공됩니다.
- 실시간으로 저장되는 로그 정보를 로그레벨, 키워드, 기간 등 다양한 조건으로 통합 검색이 가능하며 발생되는 시간대별로 저장하여 차트를 통해 확인할 수도 있습니다.
- 빠른 필터 기능도 제공하여 빠르게 로그 검색이 가능합니다.

Mobile App Crash
- ELSQ의 가장 강력한 기능은 모바일 앱크래시 정보를 쉽게 파악할 수 있다는 것입니다. ELSA에서는 iOS와 안드로이드 단말의 크래시 정보를 확인할 수 있으며 기본적으로 24시간 이내에 발생한 크래시 상세로그 및 크래시 횟수를 그래프 형태로 나타납니다.
```















| 항목명         | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| logLevel       | 레벨별로 로그를 출력합니다(FATAL / ERROR / WARN / INFO / DEBUG) |
| logSource      | 사용자가 설정한 [로그 소스]로 구분합니다                     |
| logType        | 사용자가 설정한 [로그 타입]으로 구분합니다                   |
| projectVersion | 사용자가 설정한 [프로젝트 버전]으로 구분합니다               |



##### Cloud Hadoop

```
빅데이터를 쉽고 빠르게 처리할 수 있는 오픈소스 기반의 분석 서비스
- standard , High-memory 타입을 제공
- standard : 4vCPU, 8GB ~ 16vCPU 32GB
- High-memory : 8vCPU 64GB ~ 32vCPU 235GB 

ObjectStorage 활용
다양한 프레임 워크 지원
- Core Hadoop, Hbase, Spark 등의 오픈 소스 프레임워크 제공
- DB query를 이용해 추출해서 넣어줌 

쉬운 클러스터 생성
- Core Hadoop : Hadoop을 사용하기 위한 기본 컴포넌트
- HBase : 대량의 병렬 분석이 가능하고 빠르게 데이터를 얻을 수 있습니다.
- Spark : 머신 러닝/데이터 분석에 용이한 프레임 워크
- Presto : 짧은 지연 시간의 임시 데이터 분석에 최적화된 오픈 소스 분산 SQL 쿼리 엔진
```



##### Cloud Search

```
사용자의 웹사이트에 필요한 검색 기능을 손쉽게 구현할 수 있도록 돕는 클라우드 기반의 개발 플랫폼입니다.
컨네이너를 기반으로 제공되기 때문에 검색 인프라를 확장하거나 축소할 수 있습니다.

리소스 모니터링
- 업로드 된 문서 크기 : 해당 시간에 업로드한 문서의 크기를 보여줍니다.
- Reindex 건수 : 색인변경, 섹션변경이 일어났을 때 해당 시점에 있었던 문서의 총 개수를 나타냅니다.
- API 호출 횟수 : 검색 API의 호출 횟수를 의미합니다.
- 검색 네트워크 사용량 : 검색 API의 네트워크 사용량을 의미합니다.
```



##### Elasticsearch

```
Elasticsearch 클러스터를 손쉽게 배포, 보호, 운영 및 확장하여 로그분석, 검색, App 모니터링 등을 수행 할 수 있도록 제공하고 있는 관리형 서비스 입니다.

- Elasticsearch Cluster는 1대의 매니저 노드와 3대 이상의 데이터 노드로 구성되어, 총 최소 4대의 서버로 구성됩니다.
- 데이터노드 수는 최대 10대까지 추가가 가능합니다.(최소 3대)
```

