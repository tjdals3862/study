

# Apache - Tomcat7

작성일 :20200720

작성자 : 박성민



### 목차

#### 0. Apache - Tomcat

#### 1. 설정과 배포

#### 2. 성능 튜닝

#### 3. Apache 웹 서버와 Tomcat 통합

#### 4. tomcat7 보안

#### 5. tomcat 문제 해결

#### 6. tomcat 업그레이드

#### 7. tomcat 고급설정





































### 0. Apache - Tomcat 

```
- 자바 기반 애플리케이션을 호스트하는 오픈소스 자바 기반 웹, 서블릿 컨테이너
- 자카르타 톰캣(Jakarta Tomcat)으로 개발됐다가 요구사항이 늘어나면서 아파치 소프트웨어 제단의 지원을 받는 아파치 톰캣이라는 별도의 프로젝트로 분리됨
```



##### apache- tomcat7 기능과 개선사항

```
웹 애플리케이션 메모리 누수 감지와 방지
- 4.x/5.x 버전의 tomcat에서는 메모리 누수 문제가 발생한다. tomcat을 재시작하지 않고 애플리케이션 로딩을 반복하면 메모리 누수 때문에 시간이 흐르면서 OutOfMemoryError 예외가 발생한다. tomcat은 메모리 누수 문제를 해결하려고 메모리와 관련된 버그와 이슈를 추적하는데 총력을 기울임
```



##### 서블릿 3.0

```
- 비동기 지원
서블릿 3.0의 비동기 지원을 tomcat7과 완벽하게 통합했다.
서버가 자원 요청의 응답을 기다리지 않아도 된다는 것이 가장 큰 장점
- 동적 설정
- 애노테이션(Annotation) 기반 설정
개발자는 프로그램 실행문과 관련이 없는 주석 형식의 프로그래밍을 포함할 수 있다.
주석 형식 프로그래밍의 큰 장점은 우베 서버를 고치지 않고도 애플리케이션 서블릿 클래스 재작성 규칙을 설정 할 수 있다.
```



##### 개선된 로깅

```
비동기 방식 파일 핸들러
- tomcat 비동기 방식의 핸들러를 이용해 지정된 스레드에서 디스크로 로그를 기록 할 수 있다. 따라서 로깅 동작이 작업 스레드에 영향을 주지 않는다

단일 행 로그 포맷터
- 단일 행 로그 포맷터는 관리자에게 용이하도록 로그를 한 행으로 기록한다.
```



##### 별칭

```
별칭을 이용해 관리자는 여러 웹 사이트를 호스트(다른 웹 서버와 의존성을 갖지 않은 상태를 유지) 할 수 있다. 뿐만 아니라 정적 컨텐츠 전체를 호스트할 수 있다.
```









##### tomcat7 설치

설치 요구 사항

```
- 자바 SE 1.6 또는 그 이후 버전
- OS 환경 변수 설정
```



##### 자바 설치

리눅스

```
리눅스 시스템에서 오라클 사이트에 접속해 JDK 다운
http://www.oracle.com/technetwork/java/javase/downloads/index.html

권한 수정
chmod 755 jdk-6u24-linux-i586.bin

설치
./jdk-6u24-linux-i586.bin
```



윈도우

```
리눅스 시스템에서 오라클 사이트에 접속해 JDK 다운
http://www.oracle.com/technetwork/java/javase/downloads/index.html

경로 설정


```

![1595226006169](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226006169.png)



JAVA_HOME PATH 설정 

```
시스템 속성 -> 환경 변수 -> 사용자 변수 편집
변수이름 : JAVA_HOME
변수 값 : 설치 경로
```

![1595226152883](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226152883.png)



##### tomcat7 설치

리눅스

```
tomcat 공식 사이트(http://tomcat.apache.org/download)에서 최신 버전 다운

압축해제
tar xvfz apache-tomcat-7.0.103.tar.gz

설정 변경
server.xml 등 설정 변경

시작
CATALINA_HOME/bin/catlina.sh start or startup.sh
종료
CATALINA_HOME/bin/catlina.sh stop or shutdown.sh
```

![1595226459834](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226459834.png)

윈도우

```
tomcat 공식 사이트(http://tomcat.apache.org/download)에서 최신 버전 다운

시스템 속성 -> 환경 변수 -> 사용자 변수 편집
- JDK 경로 설정
- CATALINA_HOME 설정
```

![1595226591118](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226591118.png)

![1595226669929](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226669929.png)

![1595226683268](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1595226683268.png)









### 1. 설정과 배포

##### 설정파일

```
catalina.policy
- 톰캣 7의 보안 정책 권한을 설정하는 파일. JVM이 웹 애플리케이션에 어떤 보안 정책 권한을 적용할지를 결정한다.

catalina.properties
- 이 파일은 서버를 시작할 때 검색하는 서버, 공유 로더, JAR 등의 공유 정의를 포함한다.

server.xml
- 톰캣의 중요 설정 파일 중 하나로 IP 주소, 포트, 가상 호스트, 컨텍스트 경로 등과 같은 중요 정보를 포함

tomcat-users.xml
- 역할에 기반한 정의에 따라 인증, 승인에 사용하는 파일
- 데이터베이스의 사용자/암호/역할을 이용한 인증과 컨테이너로 관리되는 보안 구현에 사용된다.

logging.properties
- 톰캣 인스턴스의 로깅 프로퍼티를 정의

web.xml
- 톰캣 인스턴스가 시작될 때 모든 애플리케이션의 기본 값을 정의

context.xml
- 애플리케이션을 실행할 때 이 파일의 내용을 로드한다.
```



##### JDBC

```
자바 데이터베이스 연결(Java Database Connectivity)은 자바 기반 데이터베이스 접근 기술로 클라이언트가 서버 데이터베이스에 접근하는 데 필요한 API를 제공한다
```



##### JNDI

```
자바 네이밍과 디렉터리 인터페이스(Java Naming and Directory Interface) 서비스는 자바 프로그래밍 언어를 사용해 만들어진 애플리케이션에 네이밍, 디렉터리 기능을 제공하는 자바 플랫폼 API다
```



##### DataSource

```
JDBC API를 이용해 관계형 데이터 베이스에 접근할 때 사용하는 자바 객체
```









##### tomcat 관리자 설정

tomcat 관리자 기능 

- 원격으로 새 애플리케이션 배포
- 아이들 세션 청소
- 컨테이너 재시작없이 애플리케이션 배포 철회
- 메모리 누수 분석
- JVM 상태
- 서버 상태



![1594802068106](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594802068106.png)



##### Server Status

- JVM status
  - JVM 상태
  - 최대 메모리
  - 총 메모리
  - 자유 메모리
- AJP 포트 8009 연결
  - 연결 상태
  - 송신 데이터
  - 수신 데이터
  - 클라이언트
  - 가상 호스트
- HTTP 포트 8080 연결
  - 연결 상태
  - 송신 데이터
  - 수신 데이터
  - 가상 호스트
- 서버 정보
  - 톰캣 버전
  - OS 버전
  - JVM 버전
  - 시스템 아키텍처





##### Context path

```
WAS에서 웹어플리케이션을 구분하기 위한 path
```



Context path 장점

- 서버의 부하를 최소화 할 수 있다
- 불필요한 검색을 피해 CPU 사이클을 절약할 수 있다
- 로깅, appBase, DB 연결 등과 같은 요구사항에 따라 애플리케이션을 자유롭게 커스터마이즈 할 수 있다.



Context 경로 활성화

1. tomcat 관리자 GUI 이용

![1594861496997](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594861496997.png)



2. server.xml 설정

   ![1594861974184](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594861974184.png)

```
path="/sample"
- 서버 요청 URL 경로를 정의

docBase="/opt/" 
- 컨텍스트 경로의 문서 루트를 정의한다

reloadable="true
- 파라미터 값이 참이면 WAR 파일이 바뀔 때마다 톰캣을 재시작하지 않고 자동을 변경사항을 적용한다

swallowOutput="true"
- 파라미터 값이 참이면 System.out과 System.err 출력을 애플리케이션 로그로 재전송한다
```









### 2. 성능 튜닝

 

##### tomcat7의 성능에 영향을 주는 요소

- 애플리케이션 코드
- 데이터베이스 튜닝
- JVM 튜닝
- 미들웨어 서비스
- 인프라 구조와 OS



##### tomcat 컴포넌트 튜닝

tomcat7의 커넥터 종류

- 자바 HTTP 커넥터
- 자바 AJP 커넥터
- APR (HTTP/AJP) 커넥터



##### tomcat7 ThreadPool 최적화

```
ThreadPool 
- 웹 서버가 수락할 수 있는 연결 수 또는 서버가 수락 할 수 있는 요청 수
- 공유(Shared)풀과 전용(Dedicate)풀 두 가지로 나뉜다
- server.xml을 이용해 설정
```



공유 ThreadPool

```
service 섹션에 공유 스레드 풀 정의를 추가
<Excutor name = "tomcatThreadPool"
namePrex="catalina-exec-"
maxThreads="150"
minSpareThreads="4"/>

공유 ThreadPool을 정의 후 service 섹션에 커넥터 정의에서 Thread 설정 참조를 호출
<Connector executor="tomcatThreadPool"
port="8080" protocol="HTTP/1.1"
connectionTimeout="20000"
redirectPort="8443"/>
```



전용 ThreadPool

```
ThraedPool을 특정 커넥터 전용을 할당하는 것
```



| 기능      | 공유 스레드 풀 | 전용 스레드 풀 |
| --------- | -------------- | -------------- |
| 사용자 수 | 적음           | 많음           |
| 환경      | 개발           | 제품           |
| 성능      | 낮음           | 좋음           |



```
maxThreads
- 서버가 수락할 수 있는 최대 요청 수를 정의한다
- 기본 설정 값은 maxThreads=150

서버 CPU 사용량을 확인해 높으면 Thread값을 줄이고 보통일 경우 더 많은 사용자 요청을 수락할 수 있도록 Thread값을 증가 시킬 수 있다.
```



```
maxKeepAlive
- 동시에 대기할 수 있는 TCP 연결 수를 정의
- 기본 값은 1, 비활성화

maxKeepAlive = 1
- tomcat에서 SSL 터미네이션을 수행하지 않는다
- 부하 균형 기법을 사용한다
- 동시에 더 많은 사용자를 수용한다

maxKeepAlive > 1
- tomcat에서 SSL 터미네이션을 수행한다
- 적은 동시 사용자를 수용한다
```



##### JVM 튜닝

```
tomcat7은 256MB 힙을 포함하지만 최근 애플리케이션은 점점 많은 램을 요구하기 때문에 JVM 파라미터를 튜닝해야한다
- tomcat의 PID 값을 확인 후 jmap을 이용해 메모리 값 확인 
```



##### JMAP(메모리 맵)

```
공유된 자바 가상 메모리 전체 모습을 출력하는 유틸
```



| 옵션            | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| -dump           | 자바 힙을 hprof 바이너리 형식으로 덤프                       |
| -finalizer info | 소멸(finalization)을 기다리는 오브젝트 정보 출력             |
| -heap           | 힙 요약 정보 출력                                            |
| -histo          | 힙 히스토그램 출력                                           |
| -permstat       | 자바 힙의 영구 세대(permanent generation)를 클래스 로더 통계로 출력 |

```
jmap -heap <PID값>
```

![1594864840779](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594864840779.png)

```
- 애플리케이션의 힙 설정
- 각 JVM 컴포넌트의 힙 사용 현황
- 가비지 콜렉션에 사용하는 알고리즘
```



tomcat7 힙 크기 증가시키는 방법

```
TOMCAT_HOME/bin/catalina.sh에 JAVA_OPTS 파라미터 추가

JAVA_OPTS="-Xms128m -Xms512m -XX:MaxPerSize=256m"
```

JVM 옵션

- 행동 옵션 : VM의 기본 행동을 바꾸는 옵션이다
- 성능 튜닝 옵션 : VM의 성능을 최적화 시키는 옵션
- 디버깅 옵션 : VM 정보를 출력하고 표시한다. 로그 추적 기능 활성화 관련 옵션







| 옵션        | 파라미터                            | 설명                                                         |
| ----------- | ----------------------------------- | ------------------------------------------------------------ |
| 행동 옵션   | -XX:+ScavengeBeforeFullGC           | 전체 GC에 앞서 젊은 세대 GC를 수행                           |
|             | --XX:-UseParallelGC                 | 병렬 가비지 콜렉션으로 빠른 GC 수행                          |
| 성능 옵션   | -XX:MaxNewSize=size                 | 신세대의 최대 크기(바이트 단위)                              |
|             | -XX:MaxPermSize=64m                 | 영구 세대의 크기(--Xmx 값을 초과했을 때)                     |
|             | -Xms                                | 톰캣 시작시 최소 힙 메모리                                   |
|             | -Xmx                                | 인스턴스에 할당할 최대 메모리                                |
|             | -Xss                                | 힙의 스택 크기                                               |
| 디버깅 옵션 | -XX:CITime                          | JIT 컴파일러가 소비한 시간 출력                              |
|             | -XX:ErrorFile=./hs_err_pid.log      | 발생한 에러를 기록할 파일 지정                               |
|             | -XX:HeapDumpPath=./java_pid.hprof   | 힙 덤프용 디렉터리 경로나 파일명                             |
|             | -XX:-HeapDumpOnOutOfMemoryError     | java.lang.OutOfMemoryError가 발생하면 힙을 파일로 덤프       |
|             | -xx:OnError="<cmd args>;<cmd;args>" | 치명적 에러 발생시 사용자가 정의한 명령 실행                 |
|             | -xx:OnOutMemoryError="<cmd args>;"  | 처음으로 OutOfMemoryError가 발생하면 사용자가 정의한 명령 실행 |
|             | -XX:-PrintClassHistogram            | Ctrl-Break를 눌렀을 때 클래스 인스턴스의 히스토그램 출력     |

##### OS 튜닝

```
64비트 VM과 32비트 VM 성능 특성 비교
- 32비트 VM이 64비트 VM보다 더 빠르지만 64비트 VM은 더 큰 메모리를 사용할 수 있다
- 64비트 JVM을 사용하려면 32비트 JVM에 비해 30퍼센트의 메모리를 더 추가해야 한다

파일 크기
- 애플리케이션의 요구사항에 따라 OS가 파일 크기를 설정한다

제한 해제
- 세션별로 사용자가 제한을 증가 시킬 수 있다.
```







### 3. Apache 웹 서버와 Tomcat 통합



#### ajp 연동

##### mod_jk 설정

1. apache 설치

```
openssl 컴파일
./config --prefix=/usr/local/openssl-1.0.1u  shared
make && make install
```



```
apache 컴파일
vi +/"#define DEFAULT_SERVER_LIMIT 256" ./server/mpm/prefork/prefork.c
256 -> 1024
./configure \
--prefix=/usr/local/httpd-2.2.23 \
--enable-modules=all \
--enable-ssl \
--enable-so \
--with-ssl=/usr/local/openssl
make && make install
```



2. mod_jk 설치

```
tar xvfz mod_jk_1.2.37-x86_64.tar.gz
mv mod_jk.so /usr/local/httpd/modules/
```

mod_jk.conf 파일 생성

```
vi /usr/local/httpd/conf/mod_jk.conf
<IfModule mod_jk.c>
        JkWorkersFile "/usr/local/httpd/conf/workers.properties"
        JkLogFile "/home/insight/tomcat/logs/mod_jk.log"
        JkLogLevel info
        JkAutoAlias "/home/insight/tomcat/webapps"
        JkMount /* ajp13
        JkMount /*.jsp ajp13
        JkMount /servlet/* ajp13
        JkMount /examples/*.jsp ajp13
        JkLogStampFormat "[%a %b %d %H:%M:%S %Y]"
        JkOptions +ForwardKeySize +ForwardURICompat -ForwardDirectories
        JkRequestLogFormat "%w %V %T"
</IfModule>
```



```
mod_jk.conf
모듈 경로 
- 아파치를 시작할 때 모듈을 로드할 위치를 정의
ex) LoadModule jk_module module/mod_jk.so

작업자 파일 경로
- 작업자 파일 위치를 정의. 작업자 파일은 톰캣 인스턴스의 IP, 포트, 로드 분산 방법 등의 정보를 포함
ex) JKWorkersFile conf/workers.properties

로그 파일
- 로그 파일은 아파치 톰캣 통합 과정이 기록
ex) JKLogFile logs/mod_jk.log

URL 매핑
- URL 매핑은 아파치 컨텍스트 경로, 정의된 URL 요청 재전송 규칙을 정의
ex) JKMount /sample/* node1

로그 수준
- 로그 수준은 파라미터 mod_jk에서 수행하는 다양한 이벤트를 logs가 어떻게 처리할지를 정의한다
ex) JKLogLevel info
```



JkWorkersFile, JkLogFile, JkAutoAlias tomcat 설치 위치에 맞춰서 수정

JkWorkersFile의 workers.properties 파일은 apache/conf에 생성

```
vi /usr/local/httpd/conf/httpd.conf

아래 두 줄 추가
LoadModule jk_module modules/mod_jk.so
Include conf/mod_jk.conf
```



workers.properties 파일 생성

```
workers.tomcat_home="/home/insight/tomcat" //tomcat 경로
workers.java_home="/home/insight/java" //jdk 경로
ps=/ 
worker.list=ajp13
worker.ajp13.port=8009  // ajp port
worker.ajp13.host=localhost //ajp host ip
worker.ajp13.type=ajp13
```



```
workers.properties
- 노드 이름(호스트의 공통 이름)
- 톰캣의 AJP 포트 세부 정보
- 톰캣 호스트
- 사용중인 프로토콜
- 부하 분산 방법
```



tomcat server.xml  수정

```
    <Connector protocol="AJP/1.3"
               address="0.0.0.0"
               secretRequired="false"
               port="8009"
               redirectPort="8443" />
```



service restart

```
apache, tomcat 순으로 재시작
```



![1594875233812](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594875233812.png)



##### mod_proxy 설정

1. http.conf 설정

```
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
```























2. VirtualHost 설정

```
NameVirtualHost *
<VirtualHost *>
	ServerNmae abc.com
	ProxyRequests off
	<Proxy *>
		Order deny,allow
		Allow from all
	</Proxy>
	ProxyPass / http://localhost:8080/
	ProxyPassReverse / http://localhost:8080/
	<Location />
		Order allow,deny
		Allow from all
	</Loation>
<VirtualHost *>
```

3.  서비스 재시작



##### mod_jk와 mod_proxy 비교

| 기능            | mod_jk        | mod_proxy                        |
| --------------- | ------------- | -------------------------------- |
| 부하 분산       | 고수준        | 기본                             |
| 인터페이스 관리 | 네            | 아니오                           |
| 컴파일          | 별도 프로세서 | 불필요. 기본적으로 아파치에 포함 |
| 설정            | 큼            | 기본                             |
| 프로토콜        | AJP           | HTTP/HTTPS/JAP                   |
| 노드 실패       | 진보          | 불가                             |



### 4. tomcat7 보안

- tomcat 보안 권한
- 카탈리나(Catalina) 속성
- tomcat7 SSL 구현



##### tomcat 보안 권한

```
catalina.properties
- 패키지 접근 관련 정보, 패키지 정의, 공통 로더, 공유 로더, 톰캣 시작시 스캔할 필요가 없는 JAR 파일 목록 등의 정보를 포함한다
```



```
catalina.policy
- 톰캣에 배포된 애플리케이션과 이들의 세부 권한 정보를 포함한다
```



```
카탈리나(Catalina) 정책
시스템 코드 권한
- 자바 라이브러리 접근 권한과 관련된 정책 

Catalina 코드 권한
- 코드에 접근하는 톰캣 내부 파일 권한을 포함하는 섹션이다

웹 애플리케이션 권한
- 애플리케이션의 자원(JVM, JNDI 등) 활용과 관련한 정책을 포함하는 섹션 
```

![1594876984684](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594876984684.png)



![1594876923667](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594876923667.png)

![1594877024575](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594877024575.png)



```
tomcat-users.xml
- 롤(role)과 보안 암호를 포함하는 파일
```

![1594877127023](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594877127023.png)



```
server.xml
- 주요 설정파일로 커넥터 포트 설정 정보를 포함한다
```

![1594877153458](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594877153458.png)









##### tomcat 설정

커넥터 포트

```
tomcat은 기본적으로 HTTP 프로토콜 8080 포트에서 실행된다. 모든 사람들이 기본 포트를 알고 있으므로
보안상 가능하면 커넥터 포트와 AJP 포트를 바꾸는 것이 좋다
```



tomcat 애플리케이션 최적화

```
tomcat7 패키지는 많은 애플리케이션과 예제를 포함한다. 사용하지 않는 애플리케이션 페이지는 삭제할 것을 권장한다
삭제 시 장점
- JVM 메모리 사용 감소
- 원하지 않는 애플리케이션을 사용할 수 없으므로 취약성 감소
- 애플리케이션 유지보수 쉬워짐
```



핫 배포 비활성화

```
서비스를 재시작 하지 않고도 애플리케이션에 자동으로 코드를 배포하는 과정을 핫 배포 또는 자동 배포라고 한다. server.xml에서 핫 배포를 비활성화 할 수 있다.
```

```
수정 전
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
            
수정 후
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="false">
            
autoDeploy : true -> false            
```



##### tomcat7 SSL 설정 

```
SSLEnabled = true
scheme = https
keystoreFile = 인증서 경로
keystorePass = 인증서 패스워드
sslProtocal = 사용 protocol

설정 후 재시작
```

![1594877573331](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594877573331.png)

![1594877717115](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594877717115.png)











### 4. tomcat 문제 해결



##### 공통 문제 영역

```
애플리케이션
- 클래스 로더 충돌, 애플리케이션 배포 충돌, 설정 파라미터 부족 등의 이유로 애플리케이션이 정상적으로 작동하지 않는 상황

데이터베이스
- 웹 관리자의 입장에서 데이터베이스 문제는 매우 중요하다. DB와 관련한 문제는 찾기 어렵다. JNDI 찾을 수 없음, 망가진 파이프 에러 등의 문제가 데이터베이스와 관련하여 발생 할 수 있다.

사용자 접근
- 데이터베이스나 애플리케이션 설정 때문에 접근 문제가 발생 할 수 있다.

네트워크
- IT 인프라구조에서 네틍워크는 핵심 역할을 한다. 서버간의 연결이 끊어지면 통신을 할 수 없으므로 서비스가 중단 된다

OS/하드웨어
- OS/하드웨어는 애플리케이션 계층의 아래쪽 계층을 구성한다. OS/하드웨어 계층에 문제가 생기면 톰캣 서버의 서비스에도 영향을 받는다.
```



##### 문제 해결 방법

```
문제 해결을 위해서는 문제의 원인을 좁혀가며 해결해야 한다.
```



1. 애플리케이션이 느려지는 문제

- 애플리케이션 실행이 너무 느린 문제



##### 문제 해결

사용자 입장에서 문제 해결

```
- 사용자의 브라우저에서 애플리케이션에 접근을 시도해서 애플리케이션 페이지를 로드하는 시간 확인
- ping 명령어를 이용해 서버 핑 확인
  전송 패킷 수와 수신 패킷수가 같아야 한다(다를 시 네트워크의 문제가 있음을 가르킨다)
  패킷 손실이 없어야 한다(0% loss)
```











웹 서버 문제 해결

```
- 웹 서버 프로세서가 정상 실행 중인지 확인
  프로세스 수와 상태 확인 
- cpu 활동상태와 메모리 상태 확인
 top|head
- error, access log 확인
- 디스크 용량 확인
  로그 파일로 인해 디스크 문제가 발생할 수 있음
```



tomcat 7 문제 해결

```
- tomcat java 프로세스와 인스턴스 평균 로드 확인
  ps -ef | grep java
- tomcat log 확인
CATALINA_HOME/log/catalina.out
grep ERROR calina.out
```



데이터베이스 수준에서 문제 해결

```
웹 관리자가 데이터베이스에 접근할 수 없는 상황도 고려해 확인
telnet DB 서버 IP 포트

DB 접속 확인 후 확인
- 데이터베이스 연결 수
- sql 질의 최적화
- 다중 서버를 이용한 데이터베이스 부하 균형 유지
```



JVM

```
애플리케이션에서 JVM을 과도하게 이용하는 상황
jamp을 이용해 JVM 인스턴스의 메모리 할당 정보 확인

2. 튜닝 참조
jamp -heap PID
```





### 5. tomcat7 모니터와 관리

- tomcat7 모니터 방법
- tomcat 관리자를 이용한 애플리케이션 관리
- tomcat7을 모니터하는 서드 파티 유틸리티







##### 시스템 모니터링 방법

```
서드 파티 도구
- Wily, SiteScope, Nagios 등 시중에서 구할 수 있는 서드 파티 도구를 이용해 모니터링을 설정한다
- 다양한 인프라구조 컴포넌트, 도메인을 포함하는 100개 이상의 서버를 가진 기업 인프라구조 설정에 이런 종류에 모니터링 도구를 사용한다

스크립트
- 특정 시간 동안 얼마나 많은 사용자가 로그인했는지 파악하거나 애플리케이션 전용 사용자 역할을 알려고 하는 경우처럼 특별한 상황 정보를 얻으려 한다면 스크립트를 이용해 모니터링을 설정 할 수 있다.

수동
- 특정 모듈의 애플리케이션 성능이 느릴 때 사용한다
- 보통 시스템 개수가 셋 이하인 상황의 문제해결 과정에서 사용한다.
```



##### tomcat7 tomcat 관리자

1. 설정과 배포 tomcat 관리자 참조

```
tomcat 관리자는 apache-tomcat의 동작을 관리하는 기본 도구다. tomcat 관리자는 IT 관리자에게 애플리케이션을 원격으로 관리할 수 있는 기능과 시스템 모니터 기능을 제공한다.
- 관리자에게 원격 배포, 롤백, 시작, 정지 기능을 제공한다
- 애플리케이션과 서버의 자세한 모니터링 상태를 제공한다
```



##### tomcat7 JConsole 설정

```
JDK 1.5 이후 버전의 JDK에서 제공하는 모니터링 유틸리티
- 로우 메모리(메모리 부족이 발생할 수 있는 상황)검출
- GC, 클래스 로딩 상세 정보 출력을 활성화하거나 비활성화
- 데드락 검출
- 애플리케이션의 모든 로거의 로그 수준 제어
- OS 자원 접근 - 썬의 플랫폼 확장
- 애플리케이션의 메니지드 빈 관리
```



```
catalina-jmx-remote.jar 설치
wget http://apache.tt.co.kr/tomcat/tomcat-7/v7.0.105/bin/extras/catalina-jmx-remote.jar

bin/setenv.sh
#!/bin/sh
 
JMX_OPTS=" -Dcom.sun.management.jmxremote \
                 -Dcom.sun.management.jmxremote.authenticate=false \
                 -Djava.rmi.server.hostname=172.16.10.30 \
                -Dcom.sun.management.jmxremote.ssl=false "
CATALINA_OPTS=" ${JMX_OPTS} ${CATALINA_OPTS}"

server.xml의 Listner 추가

<Listener className="org.apache.catalina.mbeans.JmxRemoteLifecycleListener"
        rmiRegistryPortPlatform="9840" rmiServerPortPlatform="9841"/>
        
jconsole 구동
JAVA_HOME/bin/jconsole
```



Local 진행일시 PID 값 확인

Remote Process일 시 tomcat server ip 지정

![1594881330485](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594881330485.png)



![1594881182798](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1594881182798.png)



### 6. tomcat 업그레이드

- 업그레이드 과정 생명주기



##### tomcat 6 -> 7 업그레이드

##### tomcat7의 기능 제공

- 서블릿 3.0

  - 비동기 지원
  - 동적 설정
  - 확장 서블릿 API
  - 보다 간단하고, 빠르며, 개발자 친화적
  - 단순화된 임베딩
  - 개선된 로딩

  

- 시스템 개선
  - 메모리 누수 해결
  - 보안 개선









업그레이드 방식

```
기존의 tomcat6를 실행 중인 시스템 이용
- 새 버전에서 발생하는 부하를 처리 할 수 있을 만큼 충분한 램과 CPU를 장착한 하이앤드 서버가 있을 때 이용할 수 있는 방법

별도 시스템 이용
- 최근 IT 인프라구조에서는 가상화가 인기를 끌면서 대부분이 이 방법을 사용. tomcat7의 새 버전의 부하만 처리할 로우엔드 서버를 만든다
```



tomcat7 요구 사항 확인

```
tomcat7은 JDK 1.6에서 실행되므로 JDK 설치진행
```



tomcat7 설정

- JVM 설정

```
- 현재 tomcat6에서 얼마나 많은 애플리케이션을 실행 중인가
- 동시 사용자 수
- 현재 설정
- 32비트에서 64비트로 업그레이드

메모리 할당 비교
- tomcat6,7 메모리 할당 부분에서는 큰 차이가 없으나 최신 버전 개선된 기능을 지원해야 하므로 기존 버전보다 더 많은 JVM 메모리를 할당해야 한다.
```

- 데이터베이스 연결 설정

```
tomcat6
<Resource name="jdbc/myoracle" auth="Container"
type="javax.sql.DataSource" driverClassName="oracle.jdbc.OracleDriver
"url="jdbc:oracle:thin:@192.168.0.1.:1521:mysid"username="scott"
password="tiger" maxActive="20" maxIdle="10" maxWait="-1" />

tomcat7
<Resource name="jdbc/myoracle" auth="Container"
type="javax.sql.DataSource" driverClassName="oracle.jdbc.
OracleDriver" url="jdbc:oracle:thin:@192.168.0.1.:1521:mysid"
username="scott" password="tiger" maxActive="50"
maxIdle="10" maxWait="-1" />
```













###  7. tomcat 고급설정

- 가상호스팅
- 캐시 튜닝



##### 가상 호스팅

```
하나의 웹 서버나 하나의 IP에서 여러 개의 도메인명을 제공할 수 있게 하는 기법
- 이름 기반 가상 호스팅
- IP 기반 가상 호스팅
```



##### 이름 기반 가상 호스팅

```
하나의 IP에 여러 도메인을 호스트 할 수 있는 방법이다

<Host name = "www.xyz.com" appBase="webapps"
        unpackWARs="true" autoDeploy="true">
        <Context path="" docBase="."/>
      </Host>

autoDeploy
- "true"이면, Host는, 필요에 따라서, 동적으로 웹 애플리케이션을 배치 또는 업데이트를 시도

unpackWARs
- 속성이 "false"로 되어 있다면 .WAR 파일의 압축은 풀리지 않고, 웹 애플리케이션은 단지 압축된 채로 재배치됩니다
```



##### document 설정

##### <Context> 태그의 사용

```
<Context> 태그를 사용해 appBase 하위 디렉토리를 Document Root로 지정 할 수 있다.

<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true"
            xmlValidation="false" xmlNamespaceAware="false">
    <Context path="" docBase="web" reloadable="true"/>
```



##### 원하는 디렉토리를 Document Root로 사용

```
appBase를 절대 경로로 지정하고 docBase를 현재 디렉토리로 설정
<Host name="localhost"  appBase="/home/user/oramaster/public_html"
            unpackWARs="true" autoDeploy="true"
            xmlValidation="false" xmlNamespaceAware="false">
    <Context path="" docBase="." reloadable="true"/>
..
 </Host>
  
  
 appBase를 기본값으로 나두고 docBase를 절대경로로 지정하여도 된다.
 <Host name="localhost"  appBase="webapps" 
            unpackWARs="true" autoDeploy="true"
            xmlValidation="false" xmlNamespaceAware="false">
    <Context path="" docBase="/home/user/oramaster/public_html" reloadable="true"/>
..
 </Host>
```



##### IP 기반 가상 호스팅

```
여러 IP를 이용해 하나의 서버에 여러 웹 사이트를 호스트할 때 IP 기반 가상 호스팅을 사용한다
```



