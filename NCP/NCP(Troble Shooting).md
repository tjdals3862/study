### NCP(Troble Shooting)



##### 적절한 용량 산정

```
컴퓨팅 파워
- IO Wait이 발생하는 시점부터 서비스 품질은 떨어지기 시작(CPU,memory)
- SWAP을 사용하는 경우 메모리 증설
- 관련 명령어 : sar, ps, top

네트워크
- 동접 기준으로 파일(페이지)를 기한내에 전송할 수 있을지를 가지고 선정
- 서버의 경우 전송 속도 500Mbps 기준으로 서버 대수 산정
- CDN의 경우 가용량 기준으로 산정

용량 산정 주요 지표
- 파일(페이지) 크기
- 동접
```



##### 클라우드에서의 용량 산정 전략

```
1. Scale Out 전략
- 서버의 증감이 자유롭도록 설계

2. 초기에 과투입 후 서서히 리소스를 축소
- 초기에 서비스가 필요로 하는 리소스보다 많은 리소스를 투입한 후 서비스 안정화 되면 리소스를 적정 수준까지 축소하는 전략
```



##### 성능 측정

```
웹서비스
- WMS : 부하,동접x  현재상태만o
- Ngrinder : 부하o, 동접 몇명까지 처리가능한지 확인
- Pinpoint : 어느부분에서 병목발생이 되는지
- AB

MySQL 성능측정 - 하드웨어측정
- Percona TPCC
- sysbench
- Apache Jmeter
```



##### AB

```
AB의 설치
yum install httpd-tools

AB 옵션
-n : 요청수
-c : 동시에 요청하는 요청 수
-g : 측정한 모든값을 gunplot 혹은 TSV 파일로 기록
-t : 선능을 검사하는 최대 시간 (초단위)
   4 : 헤더에 대한 정보
   3 : 응답 코드
   2 : 정보
-x : 프록시 서버를 사용하여 요청
```



##### 문제 진단을 위해 활용가능한 상품

```
웹서비스
- WMS
- Pinpoint

DB
- Cloud for Mysql
    DB Dashboard
    OS Dashboard
    DB Logs
    Query TimeLine(특정시간대의 query 확인)
    
- Cloud for MS-SQL
    DB Dashboard
    Performance
    DB Logs
    

```



#### 문제해결을 위한 명령어들

```
Linux
- tcpdump
- Nmap
- Traceroute
- sar
- ps
- lsof

Window
- Microsoft Message Analyer
- 이벤트 뷰어(eventvwr)
- Performance Monitor(perfmon)
- PSTools
```



##### sar

```
- 리소스 사용량에 대한 로그 조회
- Linux에서 시스템에 대한 광범위한 모니터링
- CPU 사용률, 메모리, iowait, 로드를 비롯한 다양한 정보를 확인 가능

sar -A
sar -b(I/O)
sar -n(network)
sar -w(컨텍스위칭)
```



##### Ping

```
- ICMP를 이용한 프로그램
- 해당 호스트가 살아있는지 죽어 있는지
- 방화벽에 의해 막혀 있는지 확인하기 위해 사용하는 기초적인 명령어
- Windows와 Linux에서의 옵션은 서로 상이
```



##### nmap

```
- 포트스캔용 툴
- 오픈되어 있는 포트에 대해 스캔
- 호스트 뿐만 아니라 대역으로도 탐지
- 응용프로그램 버전 및 OS 탐지
- Linux와 Windows 버전 사용 가능
```



##### 사용법 : nmap [Scan Type(s)] [Option] [target specification]

스캐닝 방법

```
can type	-sS	TCP SYN(Half-Open) Scan, 스텔스 스캔	　	　	　	　	　	
-sT	TCP ConnecT(Open) Scan	　	　	　	　	　	　	
-sU	UDP  Scan	　	　	　	　	　	　	　	
-sF	TCP FIN Scan : FIN 패킷을 이용한 스텔스 스캔	　	　	　	　	
-sX	TCP Xmas Scan : FIN, PSH, URG 패킷을 이용한 스텔스 스캔	　	　	　	
-sN	TCP NULL Scan : NULL 패킷을 이용한 스텔스 스캔	　	　	　	　	
-sA	TCP ACK Scan	　	　	　	　	　	　	　	
-sP	Ping(icmp/icmp echo)  Scan : Ping을 이용해 호스트 활성화 여부 확인	　	　	
-D	Decoy(유인) Scan : 실제 스캐너 주소 외에도 다양한 주소로 위조하여 스캔하는 방식	　	
-b	TCP FTP Bounce Scan, -b <FTP bounce proxy>	　	　	　	　	
　										　	
Port Option	-p 22 : 22번 포트 스캔	　	　	　	　	　	　	　	
-p  <service>  :  특정 서비스명( 예:ssh) 으로 스캔	　	　	　	　	
-p 21,25,80 :  21,25,80 번 포트 스캔, 여러 포트 스캔	　	　	　	　	
-p 1-1023 : 1~1023 번 일정범위로 포트스캔	　	　	　	　	　	
-pT21,25,80,U:53  :  TCP21,25,80번 포트와 UDP53번 포트를 분리해서 스캔	　	　	
　										　	
Output
Option	-v : 상세 내역 출력	　	　	　	　	　	　	　	
-d : Debugging	　	　	　	　	　	　	　	　	
-oN  <file> : 결과를 일반 파일 형식으로 출력	　	　	　	　	　	
-oX  <file>  : 결과를 XML 파일 형식으로 출력	　	　	　	　	　	
-oG <file>  : 결과를 Grepabel(grep, awk등으로 분석하기 편한) 파일 형식으로 출력	　	
-oA  <Directory> : 일반(.nmap), XML(.xml) Grepable(.gnmap) 파일로 출력	　	　	
　										　	
기타 Option	-O : 영문 대문자O , 대상 호스트의 운영체제 정보를 출력	　	　	　	　	
-F : 빠른 네트워크 스캐닝	　	　	　	　	　	　	　	
-T0 ~ T5 : T0 아주 느리게 ~ T5 아주 빠르게	　	　	　	　	　	
　										　	
Target	▶ hostname 지정	　	　	　	　	　	　	　	
   ex) www.todd.pe.kr	　	　	　	　	　	　	　	
▶ IP address , Network 등 가능	　	　	　	　	　	　	
   ex) 192.168.10.100 : 특정IP 지정	　	　	　	　	　	　	
   ex) 192.168.10.0/24 : 192.168.10. 대역 지정	　	　	　	　	　	
   ex) 192.168.10.100-150 : 특정범위(100-150) IP 지정
```

##### 

```
단일 호스트 검색
- nmap 106.10.50.45 10.41.83.101
- nmap -v 106.10.50.45, 10.41.83.101

대역으로 검색
- nmap 106.10.50.45-50
- nmap 106.10.50.*
- nmap 106.10.50.0/24

방화벽 확인
- nmap -sA 106.10.50.45, 10.41.83.101

방화벽으로 보호되는 호스트에 대한 스캔
- nmap -PN 106.10.50.45, 10.41.83.101

모든 패킷 표시
- nmap -packet-trace 106.10.50.45, 10.41.83.101
```



##### TCPView

```
- Windows 시스템의 TCP/UDP에 대한 상세 정보 확인
   Process, PID, Protocol, Address/Port, State, Packet Size
- 작업중인 시스템의 오픈 된 네트워크 연결 프로세스 확인
```



##### traceroute

```
- ICMP와 TTL을 이용하여 경로를 확인하는 프로그램
- Windows에서는 tracert
- 최근의 네트웍 장비들은 ICMP에 대해 응답하지 않음
- 글로벌 환경에서 어떤 회선을 타고 가는지 확인이 필요할 경우 사용
```



##### 사용법 : traceroute [옵션] [도메인명 혹은 IP주소, 서버주소]



##### lsof

```
- 현재 프로세스가 사용(오픈)하고 있는 파일 리스트 출력
- 특정 프로세스가 CPU 점유율이 높을 경우 어떤 문제인지 확인하기 위해 사용
```



```
-a : 여러 옵션을 사용시 AND 연산으로 정보를 출력
-c : 특정 명령어를 사용하고 있는 정보를 출력
-d : 현재 사용중인 File Descriptor 기준으로 정보를 출력한다
+D : 특정 디렉토리의 열린 파일 정보를 출력한다
-F : 출력된 정보에서 원하는 필드의 정보만 출력한다
-g : 특정 그룹ID로 정보를 출력한다
-i : 특정 프로토콜과 포트 정보를 출력한다
-N : NFS에 연결되어 있는 파일 정보를 출력한다
-l : 계정이름이 아닌 UID(숫자)로 변경되어 출력한다
-n : 호스트 이름대신 IP로 정보를 출력한다
-p : 특정 PID가 참조하고 있는 프로그램 파일, 라이브러리를 출력한다
-r : 주기적으로 정보를 출력한다
-t : 동작하고 있는 프로세서들의 PID만 출력한다
-T : TCP 프로토콜로 통신하는 소켓만 출력한다
-u : 특정 계정으로 열린 파일을 출력한다
-U : UDP 프로토콜로 통신하는 소켓만 출력한다
-V : lsof 정보를 출력
```



##### tcpdump

```
- 트래픽 모니터링
- 네이버 클라우드 플랫폼의 서버들의 경우 LB로 연결된 구조의 경우 사용이 제한적
- 일반적인 사용법
  호스트 관련
   - tcpdump host
   - tcpdump src
   - tcpdump dst
   - tcpdump net
   프로토콜 관련
   - tcpdump port
   - tcpdump src port
   - tcpdump dst port
```



##### 이벤트 뷰어

```
Windows의 syslog
주로 살펴봐야 하는 항목
- Windows 로그 > 시스템
  : 시스템 Fault가 발생할 경우 이에 대한 로그 기록
- Windows 로그 > 보안
  : 시스템 로그인 내역
- Windows 로그 > 응용 프로그램
  : 응용 프로그램의 다양한 로그 기록
- 응용 프로그램 및 서비스 로그
  : 응용프로그램, 서비스에 대한 이벤트 로그 기록
```



##### 성능모니터

```
Windows의 sar
Windows 시스템의 광범위한 리소스 모니터링
- Processor
- Process
- Memory
- System
- Network Interface
- Physical Disk / Logical Disk
```



##### 커널 파라미터 변경

```
Sysctl 명령어를 이용한 변경
- Linux의 경우 커널 파라미터를 변경함으로써 성능을 변경할 수 있다.

Sysctl.conf
- 리눅스 커널 파라미터중 주요한 항목에 대한 설정

Limits.conf
- 사용자별 limit 설정
- 프로세스, 오픈 파일 등이 sysctl.conf 파일과 함께 변경되어야 효과

파일 확인
- 오픈할 수 있는 파일 개수 확인 cat /proc/sys/fs/file-nr
- 변경
   /etc/sysctl.conf
   fs.file-max = 819200
   
TCP 타임 아웃
- 확인 sysctl -a | grep keep
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_intvl = 75

Limits.conf
- 사용자별 limit 설정
- 프로세스, 오픈 파일 등이 sysctl.conf 파일과 함께 변경되어야 효과
```





































