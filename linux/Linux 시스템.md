# Linux 시스템



##### 리눅스 정보

```
uname
-a : 모든정보
-m : 하드웨어 종류
-n : 호스트 이름
-p : 소유자 이름
-r : 현재 버전
```



##### OS 정보

```
OS 버전
cat /proc/version

OS 종류
cat /etc/issue.net
cat /etc/*release*
```



##### CPU 정보

```
0. CPU 정보 확인
cat /proc/cpuinfo

1. CPU 코어 전체 개수 확인
grep -c processor /proc/cpuinfo

2. 물리 CPU 수 확인
grep "physical id" /proc/cpuinfo | sort -u | wc -l

3. CPU당 물리 코어 수 확인
grep "cpu cores" /proc/cpuinfo | tail -1
```



##### 메모리 정보

```
cat /proc/meminfo
```



##### 캐시메모리 비우기

```
sync 
echo 1 > /proc/sys/vm/drop_caches or sysctl -w vm.drop_caches=1
echo 2 > /proc/sys/vm/drop_caches or sysctl -w vm.drop_caches=2
echo 3 > /proc/sys/vm/drop_caches or sysctl -w vm.drop_caches=3

sync : 캐시메모리에 올라간 데이터를 디스크로 옮겨준다 이 과정을 진행하지 않을시 데이터 유실 발생 될 수 있다.
1 : Page Cache 비우기
2 : dentries, inodes 비우기
3 : 모두비우기
```



##### swap memory 조정

```
# cat /proc/sys/vm/swappiness : swap 빈도 확인 0 ~ 100 (0에 가까울수록 사용안함)

echo 0 > /proc/sys/vm/swappiness
```





##### 시스템 vender 확인

```
yum install dmidecode
dmidecode | more
```



##### Locale

```
프로그램을 언어와 국가에 최적화하기 위해 사용하는 "지역/언어"정보
```

- Locale 목록 확인

![1606797704440](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606797704440.png)



- 현재 Locale 정보 확인

![1606797738368](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1606797738368.png)



- locale 설정 변경

```
cat /etc/default/locale 수정
LANG=ko_KR.UTF-8
```





##### Linux 시스템 로그

- 개요

1. 리눅스에서는 /var/log 디렉터리에서 시스템의 모든 로그를 기록 및 관리하고 있다.
2. 서버에는 여러 개의 로그 파일이 있으며 이들 로그를 남기는 데몬들 또한 다양하다



- 리눅스 로그 파일

1. /var/log/dmesg 로그 파일

```
리눅스가 부팅될 때 출력되는 모든 메세지를 기록하고 있다. 부팅시 에러나 조치사항을 살펴보려면 이 파일을 참조해야 한다
```



2. /var/log/cron 로그 파일

```
- 시스템의 정기적인 작업에 대한 로그이다. 시스템 cron 작업에 대해 기록하고 있는 파일
- /etc/conr (houly/daily/weekly/monthly) 디렉터리들은 시간별, 일별, 주별, 월별로 정기적으로 운영체제에서 자동 실행할 작업 스크립트 파일들이 존재한다
```



3. /var/log/messages 로그 파일

```
- 리눅스 시스템의 가장 기본적인 시스템 로그파일로서 시스템운영에 대한 전반적인 메세지를 저장
- 주로 시스템 데몬들의 실행상황과 내역, 그리고 사용자들의 접속정보 등의 로그기록내역을 기록하고 있다.
```



4. /var/log/secure 로그 파일

```
- 주로 사용자들의 원격접속 정보를 기록하고 있는 로그파일이다.
- 시스템의 불법 침입 등을 의심한다면 이 로그파일을 확인해야 한다
- 주로 sshd 데몬과 su 관련 실행, 그리고 telnet 관련 원격 접속 내용들이 기록된다.
```



5. /var/log/xferlog 로그 파일

```
- 리눅스 시스템의 FTP 로그 파일로서 proftpd 또는 vsftpd 데몬들의 서비스 내역을 기록하는 로그 파일이다
```



6. /var/log/maillog 로그 파일

```
- sendmail 또는 qmail 등과 같은 메일 송수신 관련 내역들과 ipop또는 imap 등과 같은 수신내역들에 대해 기록되는 로그 파일이다
```



7. /var/spool/mail 로그 파일

```
- 사용자들에 대한 메일을 보관하고 있는 디렉터리로서 메일을 한번 이상 사용한 사용자는 사용자 계정 ID와 동일한 파일이 하나씩 존재한다
- 사용자 계정 생성 시 /var/spool/mail 디렉터리 내에 생성하는 계정명과 동일한 메일 파일이 생성된다.
```



#### OOM Killer

```
Out Of Memory Killer의 약자로 메모리가 부족할 경우 특정 프로세스를 강제로 종료시킵니다.

OOM이 발생하는 경우 /var/log/messages 경로에 메세지가 기록됨

Aug 13 10:33:31 insightdb kernel: mysqld invoked oom-killer: gfp_mask=0x280da, order=0, oom_adj=0, oom_score_adj=0
Aug 13 10:33:31 insightdb kernel: [<ffffffff81122de2>] ? oom_kill_process+0x82/0x2a0
Aug 13 10:33:31 insightdb kernel: [ pid ]   uid  tgid total_vm      rss cpu oom_adj oom_score_adj name
```



OOM Killer 발생 원인

```
커널은 VM을 이용한 메모리 할당을 진행하므로, 실제 Physical 메모리보다 큰 프로그램을 구동할 수 있다.
당장 사용하지 않은 메모리는 나중에 할당하여 사용하기 때문에, 실제 메모리를 넘는 프로그램들도 구동될 수 있다. 이때 이 OverCommit 된 메모리에 쓰여지게 되는 경우 메모리가 모자라며 Out of Memory가 발생한다
```



OOM Killer 순위 설정 방법

```
1. 특정 프로세스의 PID를 조회
2. /proc/PID/oom_adj 파일 확인
oom_adj는 -17 ~ 15의 값을 가지며, 낮은 값 일수록 우선순위에서 밀려난다.
3. /proc/PID/oom_score_adj 파일 확인
oom_score_adj는 -1000 ~ 1000 의 값을 가지며, 낮은 값 일수록 우선순위에서 밀려난다
```























