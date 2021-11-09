### pfsense

##### 작성일 : 2020-09-25

##### 작성자 : 박성민



```
 pfSense란 FreeBSD 기반의 오픈 소스 방화벽 / 라우터 컴퓨터 소프트웨어 배포판을 말하며 ,  라우터, 스위치, 무선라우터/스위치 또는 방화벽으로 설정하여 사용할 수 있습니다.   부가적으로 DNS, DDNS, DHCP, NTP, SNMP, VPN 등의 기능을 설정할 수 있습니다.
```



##### 주요 기능

```
방화벽 및 라우터
- 상태 기반 패킷 검사(SPI)
- GeoIP 차단
- 동적 DNS
- 캡티브 포털 게스트 네트워크
- NAT 매핑(인바운드/아웃바운드)
- DHCP 서버

VPN
- IPsec 및 OpenVPN
- SSL 암호화
- 모바일 기기용 L2TP/IPsec
- 페일오버용 멀티-WAN
- VPN 터널 페일오버
- NAT 지원

침입 방지 시스템
- 스노트 기반의 패킷 분석기
- 멀티 규칙 소스 및 카테고리
- 이머징 위협 데이터베이스
- IP 블랙리스트 데이터베이스
- 딥 패킷 검사(DPI)

엔터프라이즈급 안정성
- 선택적 멀티노드 고가용성 클러스터링
- 멀티-WAN 부하 밸런싱
- 자동 연결 페일오버
- 트래픽 제어 마법사
- 트래픽 우선순위에 기반한 대역폭 확보 또는 제한

사용자 인증
- 로컬 사용자 및 그룹 데이터베이스
- 사용자 및 그룹 기반의 권한 설정
- 선택적 자동 계정 만료
- 외장 RADIUS 인증
- 반복적 시도 후 자동 폐쇄

프록시 및 콘텐츠 필터링
- HTTP 및 HTTPS 프록시
- 비투명 또는 투명식 캐싱 프록시
- 도메인/URL 필터링
- 안티 바이러스 필터링
- HTTPS URL 및 콘텐츠 스크리닝
- 도메인 이름 블랙리스트 생성(DNSBL)
```



#### 설치 

##### 1. VM setting

![1601000502932](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000502932.png)



##### 2. 설치 진행

![1601000584107](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000584107.png)

![1601000596324](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000596324.png)

![1601000628617](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000628617.png)

![1601000636605](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000636605.png)



##### 3. 초기 인터페이스 설정

##### ![1601000761384](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000761384.png)

```
– Vlan set up? n 

– WAN interface name ? 
네트워크 명 입력
ex) em0
– LAN interface name ?  
네트워크 명 입력

– Procced ? y

–  Vlan은 구성 하지않고  Wan , Lan에  각각 공인 , 사설 인터페이스 입력 (vtnet0 , vtnet1) ,  이후 인터페이스 설정 진행 
```



![1601000841924](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601000841924.png)



##### IP 설정

```
2. Set interface IP address 선택

ip, subnet, gateway 작성
```

![1601008250716](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601008250716.png)



![1601009975901](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1601009975901.png)

```
초기 관리자 계정
admin : pfsense
```

