## sar

##### 작성일 : 2020-12-01

##### 작성자 : 박성민

##### 





##### sar 설치

```
ubuntu
apt-get install sysstat

config 설정 변경
cat /etc/default/sysstat
변경 전 : ENABLED="false"
변경 후 : ENABLED="true" 

데몬 기동
/etc/init.d/sysstat start

sar 로그 디렉토리
/var/log/sysstat/

시간이 나오지 않을경우
LC_ALL=x sar

주기 설정
/etc/cron.d/sysstat
```



##### 1. sar 명령어란

```
- sar 명령어는 솔라리스,유닉스,리눅스 등에서 유용하게 쓰는 시스템 모니터링 프로그램이다.
- 모니터링 대상이 상당히 넓은 편이며 기본값은 CPU 활동에 대한 통계를 출력한다.
- 각종 활동에 대한 통계를 다른프로그램을 이용하여 파일로 저장하고 통계치를 리포팅 하는 기능을 제공한다.
- sadc에서 생성한 daily activity 파일을 읽어서 보고서를 작성하기도 하고 시스템의 활동 상황을 수집 할 수도 있다.
```

















##### 2. sar 명령어로 모니터링 가능한 목록

```
- I/O 전송량
- 페이징
- 프로세스 생성 숫자
- 블락 디바이스 활동
- 인터럽트
- 네트워크 통계
- run 큐 및 시스템 부하 평균
- 메모리와 스왑 공간 활용 통계
- 메모리 통계
- CPU 이용도
- 특정 프로세스에 대한 CPU 이용도
- inode, 파일, 기타 커널 테이블에 대한 상태
- 시스템 스위칭 활동(context switch)
- 스와핑 통계
- 특정 프로세스 통계
- 특정 프로세스의 자식 프로세스 통계
- TTY 디바이스 활동
```



##### 3. sar 명령어 활용

- ##### 기본 정보 보기

##### sar

![1604378483354](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1604378483354.png)

```
%user : 사용자 레벨(application level)에서 실행중일때의 CPU사용률(%)
%nice : 사용자 레벨(application level)에서 nice 가중치를 준 CPU 사용률(%)
%system : 시스템레벨(kernel)에서 실행중일때의 CPU 사용률(%)
%idle : CPU가 쉬고있는 시간의 %
%sys : kernel mode에서 작동한 CPU 가동률
%idle : idle 상태로 있었던 CPU 대기율
%iowait : io wait 상태로 있었던 CPU 대기율
```



- ##### 실시간 정보 보기

##### . sar [간격] [인터벌] 형식으로 입력



- ##### 버퍼의 액티비티 측정 :   I/O와 transfer의 통계를 백분율로 출력합니다.

##### sar -A : 모든 관련정보를 출력

##### sar -b : I/O 와 transfer의 통계를 백분율로 출력한다.

```
tps : 디스크에서 발생되어진 초당 전송량. 즉 디스크에 요청한 I/O양.
rtps : 디스크로부터 발생된 초당 읽기 총 요청 횟수
bread/s : 드라이브 안의 블럭에서 초당 읽은 데이터의 총합.
bwrtn/s : 드라이브 안의 블럭에서 초당 쓰여진 데이터의 총합.
```



##### sar -B : 페이징 통계 출력

![1606787595358](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606787595358.png)

```
pgpgin/s : 디스크로부터 초당 paged in 된 page의 총 수
papgout/s : 디스크에 초당 paged out 된 page의 총 수
```



##### sar -c : 새롭게 만들어져 활동하고있는 프로세스 출력



##### sar -e hh:mm:dd  : 리포터의 종료시간 설정 (기본 ending time은 18:00:00)



##### sar -i interval : 몇초간격으로 데이터를 출력할것인가를 결정



##### sar -n DEV | EDEV | SOCK | FULL : 네트워크통계를 출력



##### DEV

![1606795998688](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606795998688.png)

##### EDEV

![1606796304007](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606796304007.png)





##### SOCK

![1606796327881](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606796327881.png)

```
DEV : Network Device의 결과로 부터의 통계
- IFACE : Network Interface 이름
- rxpck/s : 초당 받은 패킷수
- txpck/s : 초당 전송한 패킷수
- rxbyt/s : 초당 받은 bytes
- txbyt/s : 초당 전송한 bytes
- rxcmp/s : 압축된 패킷을 초당 받은 수
- txcmp/s : 압축된 패킷을 초당 전송한 수
- rxmcst/s : 초당 받은 다중 패킷 수

EDEV : Network Device의 에러 통계
- IFACE : Network Interface 이름
- rxerr/s : 초당 불량 패킷을 받은 수
- txerr/s : 패킷전송중 초당 발생한 에러 수
- coll/s : 패킷전송중 초당 발생한 충돌 수
- rxdrop/s : 리눅스 buffer의 부족으로 패킷을 받는 도중 초당 drop된 패킷 수
- txdrop/s : 리눅스 buffer의 부족으로 전송중 초당 drop 된 패킷 수
- txcarr/s : 패킷전송도중 초당 발생한 carrier-error 수
- rxfram/s : 패킷을 받는도중 초당 발생한 frame alignment 에러 수
- rxfifo/s : 패킷을 받는 도중 초당 발생한 FIFO overrun 에러 수
- txfifo/s : 전송된 패킷중 초당 발생한 FIFO overrun 에러 수

SOCK : Socket의 통계
- totsck : 총 사용된 socket수
- tcpsck : 현재 사용중인 TCP socket 수
- udpsck : 현재 사용중인 UDP socket 수
- rawsck : 현재 사용중인 RAW socket 수
- ip-frag : 현재 사용중인 IP fragments 수

FULL : 모든 종류의 Keywords(DEV,EDEV,SOCK) 내용을 출력
```



##### sar -r : 메모리 & 스왑 공간의 이용 통계를 출력한다.

![1606796505229](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606796505229.png)

```
kbmemfree : 사용가능한 총 메모리의 양(kbytes)
kbmemused : 사용중인 총 메모리의 양(kbyes), 커널에서 사용중인 메모리는 제외
%memused : 사용된 메모리의 %
kbmemshrd : 시스템에서 공유메모리로 사용된 총 메모리의 양 (kbytes)
kbbuffers : 커널에서 buffer 메모리로 총 사용된 메모리의 양(kbytes)
kbcached : 커널에서 cache data로 사용된 총 메모리의 양(kbytes)
kbswpfree : 사용가능한 스왑공간의 양(kbytes)
kbswpused : 사용된 스왑공간의 양(kbytes)
%swpused : 사용된 스왑공간의 %
```



##### sar -R : 메모리 통계

![1606796739945](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606796739945.png)

```
frmpg/s : 시스템에서 초당 자유로워진 memory pages의 양
페이지의 크기는 시스템 아키텍쳐에 따라 달라지며 보통 4k / 8k 이다
shmpg/s : 시스템에서 초당 더해진 memory pages의 양
bufpg/s : 시스템에서 초당 buffer에 추가적으로 더해진 memory pages의 양
```



##### sar -s hh:mm:ss  :  명령어를 실행시킬 시작시간 설정



##### sar -v : 커널테이블 & 파일에서 inode의 상태를 출력

![1606797036684](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606797036684.png)

```
dentunusd : Directory cache에서 사용되고있지 않은 cache entries
file-sz : file handles의 사용양
%file-sz : 리눅스 커널에서 할당가능한 최대 파일핸들의 수에대한 파일핸들의 사용된 퍼센트(%)
inode-sz : inode handles의 사용양
super-sz : 커널에의해 할당된 super block handles의 수
%super-sz : 리눅스가 할당 가능한 최대 슈퍼블럭핸들에대한 실제로 할당되어진 슈퍼블랙핸들의 퍼센트
dquot-sz : Disk quota entryes의 수
```



##### sar -w : 시스템의 switching  활동 현황 출력

![1606797374768](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606797374768.png)

```
cswch/s : 초당 context switching의 수
```



##### sar -W : swapping의 통계 출력

![1606797434967](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606797434967.png)

```
pswpin/s : 초당 swap in 된 수
pswout/s : 초당 swap out 된 수
```





