# NGINX HTTP SERVER

```
작성일 : 2020-05-06
작성자 : 박성민
```



[TOC]

















### 1. nginx 설치

------



#### 1.1 source 컴파일 설치를 위한 사전 설치 진행

```
gcc
apt-get install build-essential

PCRE 라이브러리
apt-get install libpcre3 libprce3-dev

zlib 라이브러리
apt-get install zlib1g zlib1g-dev

openssl
apt-get install openssl libssl-dev

```



#### 1.2 nginx 설치

```
nginx download
wget http://nginx.org/download/nginx-1.16.1.tar.gz

tar xvfz nginx-1.16.1.tar.gz
./configure --prefix=/usr/local/nginx-1.16.1
make && make install

--prefix=설치 경로
```



#### 1.3 데몬의 시작과 종료

설치 위치에서 진행 : /usr/local/nginx/sbin/

| 명령            | 설명                        |
| --------------- | --------------------------- |
| nginx           | 데몬 시작                   |
| nginx -s stop   | 데몬을 강제로 종료          |
| nginx -s quit   | 안전하게 데몬을 종료        |
| nginx -s reopen | 로그 파일을 다시 연다       |
| nginx -s reload | 구성 파일을 다시 읽는다     |
| nginx -t        | 구문, 유효성, 무결성 테스트 |







스크립트 설치

```
vi /etc/init.d/nginx
스크립트 삽입

chmod +x /etc/init.d/nginx

데비안 기반 배포
update-rc.d -f nginx defaults

레드햇 기반 배포
chkconfig nginx on
```



### 2. 기본 엔진엑스 구성

------

- 구성 구문 표기

- 기본 구성 지시어 개요

  

#### 2.1 구성 구문 표기

기본 파일 경로 : /usr/local/nginx/conf/nginx.conf

지시어는 항상 세미콜론(;)으로 끝나야 한다

```
worker_processes 1; 
하나 이상의 값을 지정할 수 있는 설정 키

include mime.types;
mime.types를 포함시킨다

지시어 블록
events {
    worker_connections  1024; // 서버가 동시에 수용할 수 있는 연결 수
}

http {
    server {
        listen 80; // port
        server_name example.com; // domain
        access_log /var/log/nginx/example.com.log; //http 통신 log
        location ^~ /admin/ {
            index index.php;
        }
    }
}

server 블록은 가상 호스트를 구성
```



| 표준 파일명    | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| nginx.conf     | 웹 서버의 기본 구성                                          |
| mime.types     | 파일 확장자와 연관된 MIME 타입의 목록                        |
| fastcgi_params | Fast CGI 관련 구성                                           |
| proxy.conf     | 프록시 관련 구성                                             |
| sites.conf     | 엔진엑스로 제공되는 웹사이트(가상 호스트) 구성, 도메인 단위로 분리하기를 권장 |



#### 2.2 기본 구성 지시어 개요

#####  2.2.1 기반 모듈의 지시어

 기반 모듈 : 엔진엑스의 기본적인 기능을 가진 매개변수를 정의할 수 있는 지시어 제공

| 용어                            | 설명                                                     |
| ------------------------------- | -------------------------------------------------------- |
| 핵심 모듈(core module)          | 프로세스 관리나 보안 같은 필수 기능 및 지시어로 이뤄진다 |
| 이벤트 모듈(event module)       | 네트워킹 기능의 내부 동작 방식을 구성한다                |
| 구성 모듈(configuration module) | 구성을 외부 파일에서 가져와 포함시킨다                   |



### 3. HTTP 구성

------

- HTTP 핵심 모듈
- http/server/location 구조
- 주제별로 구성된 HTTP 핵심 모듈 지시어
- location 블록 상세
- vhost 설정



#### 3.1 HTTP 핵심 모듈

```
HTTP 핵심 모듈 : HTTP 서버의 모든 기반 블록, 지시어, 변수를 포함하는 구성 요소
```













#### 3.2 http/server/location 구조

```
http, server, location의 논리적 구조를 이해해야 한다.

- http : 구성 파일의 최상위에 삽입된다. 엔진엑스의 HTTP와 관련된 모듈 전부의 지시어와 블록은 http 블록에서만 정의 할 수 있다.

- server : 웹 사이트 하나를 선언 할 수 있다. 즉 엔진엑스가 특정 웹사이트를 인식하고 구성을 얻는 블록
http 블록 안에서만 사용 가능

-location : 웹 사이트의 특정 위치에만 적용되는 설정을 정의하는데 쓰는 블록
server 블록 안이나 location 블록 안에 중첩해서 사용 가능
```



#### 3.3 주제별로 구성된 HTTP 핵심 모듈 지시어

```
listen
맥락 : server
웹 port 지정

server_name
맥락 : server
server 블록에 하나 이상의 호스트 이름을 할당하는 지시어

server_name_in_redirect
맥락 : http, server, location
내부적인 경로 재설정의 경우에 적용
기본값 : off

server_names_hash_max_size
맥락 : http
서버 이름 해시 테이블의 최대 크기를 정의
기본값 : 512

server_names_hash_bucket_size
맥락 : http
서버 이름 해시 테이블의 최대 버킷 크기를 설정
기본값 : 32

port_in_redirect
맥락 : http, server, location
경로 재설정 상황에 엔진엑스가 포트 번호를 재설정되는 URL에 추가할지 여부를 지정
기본값 : on

tcp_nodelay
맥락 : http, server, location
연결 유지 상황에서 TCP_NODELAY 소켓 옵션을 활성화하거나 비활성화한다
기본값 : on

tcp_nopush
맥락 : http, server, location
TCP_NOPUSH, TCP_CORK 소켓 옵션을 활성화 또는 비활성화 한다.
기본값 : off

sendfile
맥락 : http, server, location
활성화되면 엔진엑스는 sendfile 커널 호출을 사용해서 파일을 전송하고 비활성화시 스스로 파일을 전송
기본값 : off

sendfile_max_chunk
맥락 : http, server
sendfile 호출마다 사용도리 데이터 최대 크기를 지정
기본값 0

send_lowat
맥락 : http, server
FreeBSD에서 TCP 소켓에 SO_SNDLOWAT 플래그를 사용하게 하는 옵션
기본값 : 0

reset_timedout_connection
맥락 : http, server, location
시한이 만료된 후 이 연결과 연관된 모든 정보가 삭제
기본값 : off
```



##### 3.3.1 경로와 문서

웹사이트가 제공할 문서를 구성하는 지시어

```
root
맥락 : http, server, location, if
방문자에게 제공하고자 하는 파을을 담고 있는 최상위 문서 위치를 정의
기본값 : htmlj

alias
맥락 : location
엔진엑스가 특정 요청에서 별도 경로의 문서를 읽도록 할당한다

error_page
맥락 : http, server ,location, if
HTTP 응답 코드에 맞춰 URL를 조작하거나 이 코드를 다른 코드로 대체한다

if_modified_since
맥락 : http, server, location
엔진엑스가 If-Modified-Since HTTP 헤더를 처리하는 방법을 정의한다
if_modified_since off | exact | before
기본값 : exact

index
맥락 : http, server, location
요청에 아무런 파일명도 지정되지 않았을 때 엔진엑스가 기본으로 제공할 페이지를 정의한다
기본값 : index.html

recursive_error_pages
맥락 : http, server, location
반복적인 오류 페이지 진입을 허용하거나 막는다
기본값 : off 
```



##### 3.3.2 라이언트 요청

엔진엑스가 클라이언트 요청을 처리하는 방법

```
keepalive_requests
맥락 : http, server, location
한 연결을 닫지 않고 유지하면서 제공할 최대 요청 횟수를 지정한다.
기본값 : 100

keepalive_timeout
맥락 : http, server, location
서버가 유지되는 연결을 끊기 전에 몇 초를 기다릴지 정의하는 지시어
기본값 : 75

keepalive_disable
맥락 : http, server, location
연결 유지 기능을 비활성화할 브라우저를 선택 할 수 있다.
기본값 : msie6

send_timeout
맥락 : http, server, location
지정된 시간이 지난 후에 엔진엑스가 비활성 상태의 연결을 닫는다
기본값 : 60

client_body_in_file_only
맥락 : http, server, location
지시어가 활성화되면 들어오는 HTTP 요청의 본문 데이터가 디스크에 실제 파일로 저장된다.
client_body_in_file_only on | clena | off
기본값 : off

clinet_blody_in_single_buffer
맥락 : http, server, location
엔진엑스가 요청 본문 데이터를 메모리에 있는 단일 버퍼에 저장할지 여부를 정의한다
기본값 : off

client_body_buffer_size
맥락 : http, server, location
클라이언트 요청의 본문 데이터를 보관할 버퍼의 크기를 지정
기본값 : 8k or 16k

client_body_temp_path
맥락 : http, server, location
클라이언트 요청 본문 파일이 저장될 디렉터리 경로를 정의할 수 있는 옵션
기본값 : client_body_temp

client_body_timeout
맥락 : http, server, location
클라이언트 요청 본문 데이터를 읽는 동안 적용될 비활성 시한을 정의하는 지시어
기본값 : 60

client_header_buffer_size
맥락 : http, server, location
엔진엑스가 요청 헤더에 할당할 버퍼의 크기를 정의할 수 있는 지시어
기본값 : 1k

client_header_timeout
맥락 : http, server, location
클라이언트 요청 헤더를 읽는 동안 적용될 비활성 시한을 정의
기본값 : 60

client_max_body_size
맥락 : http, server, location
클라이언트 요청 본문 데이터의 최대 크기
기본값 : 1m

large_client_header_buffers
맥락 : http, server, location
client_header_buffer_size로 정한 기본 버퍼가 부족할 경우 클라이언트 요청을 저장하는 데 사용될 대용량 버퍼의 개수와 크기를 정한다
기본값 : 4*8k

lingering_time
맥락 : http, server, location
본문이 있는 클라이언트 요청에 적용
기본값 : 30초

lingering_timeout
맥락 : http, server, location
엔진엑스가 클라이언트 연결을 닫기 전에 읽는 두 작업 사이에서 기다려야 할 시간을 정의
기본값 : 5초

lingering_close
맥락 : http, server, location
클라이언트 연결을 닫는 방식을 제어
기본값 : on

ignore_invalid_headers
맥락 : http, server
비활성화 되면 엔진엑스는 구문이 잘못된 요청 헤더가 들어올 경우 "400 잘못된 요청" HTTP 오류를 반환한다.
기본값 : on

chunked_transfer_encoding
맥락 : http, server, location
HTTP 1.1 요청을 분할 전송 인코딩을 활성화하거나 비활성화함
기본값 : on

max_ranges
맥락 : http, server, location
클라이언트가 파일의 일부 내용을 요청할 때 허용할 바이트 수의 범위를 정의


```



##### 3.3.3 제한과 제약

```
limit_except
맥락 : location
명시적으로 허용하는 것을 제외하고 모든 HTTP 메서드를 막게해준다

limit_rate
맥락 : http, server, location
개별 클라이언트 연결의 전송률을 제한할 수 있다.
기본값 : 무제한

limit_rate_after
맥락 : http, server, location, if
limit_rate 지시어가 효력을 발휘하기 전에 전송되는 데이터의 양을 정의한다
기본값 : 없음

satisfy
맥락 : location
클라이언트가 모든 접근 조건을 만족해야 하는지, 아니면 하나만 해당하면 충족되는지 정의한다.

internal
맥락 : location
location 블록을 내부용으로 지정한다.
```



#### 3.4 모듈 변수

- 요청 헤더 : 클라이언트 요청 헤더 변수의 형태로 접근하게 해준다
- 응답 헤더 : 클라이언트에 보내지는 응답의 HTTP 헤더에 접근할 수 있다.
- 엔진엑스 생성 : HTTP 헤더 외에도 엔진엑스는 요청, 요청이 처리된 방식과 앞으로 처리돼야 할 방식, 현재 구성에서 사용되는 설정에 관한 많은 변수를 제공한다.



#### 3.5 location 블록 상세

```
= 조정 부호
지정된 패턴과 정확히 일치해야 한다

조정부호 생략
요청된 문서 URI가 지정된 패턴으로 시작해야한다

~ 조정 부호
요청된 URI가 지정된 정규식에 일치하는지 비교하면서 대소문자를 구분한다

~* 조정 부호
요청된 URI가 지정된 정규식에 일치하는지 비교하면서 대소문자를 구분하지 않는다

^~ 조정 부호
조정 부호가 생략된 경우와 비슷하게 동작한다

@ 조정 부호
이름이 지정된 location 블록을 정의한다
```



#### 3.6 vhost 설정

```
가상호스트 디렉토리 생성
mkdir /var/www/vhost

test를 위해 localPC host 파일에 해당 서버 ip에 도메인 두개 등록
ex) 172.16.120.20 test1.co.kr test2.co.kr

vhost 파일 생성
기존 파일과 설정을 동일하나 server_name만 변경
vi /usr/local/nginx/sites-enable/test2.conf

server_name test2.co.kr;

nginx.conf 설정
include /etc/nginx/sites-enabled/*;
```



### 4. 모듈 구성

------

- 로그 모듈
- 접근 모듈
- Gzip 필터
- SSL 모듈



#### 4.1 로그 모듈

엔진엑스가 접근 로그를 다루는 동작 방식을 제어

```
맥락 : http, server, location

access_log
접근 로그 파일의 경로를 정한다

log_format
접근 로그의 항목에 포함될 내용을 서술하는 식으로 access_log 지시어에서 활용할 템플릿을 정의한다

open_log_file_cache
로그 파일 서술자용 캐시를 구성한다
```



#### 4.2 접근 모듈

allow와 deny라는 두 가지 지시어가 접근 모듈을 통해 제공된다

이 지시어를 통해 특정 IP 주소나 IP주소 범위에서 자원에 접근하도록 허가하거나 거절할 수 있다.

```
ex)
location {
allow 127.0.0.1; # 로컬 IP 주소를 허용
deny all; # 모든 IP 주소 차단
}
```













#### 4.3 Gzip 필터

클라이언트에 전송하기 전에 Gzip 알고리즘으로 응답의 본문을 압축할 수 있게 한다

```
맥락 : http, server, location

gzip_buffers
압축된 응답을 저장하는 데 사용될 버퍼의 개수와 크기를 정의한다

gzip_comp_level
GZip 알고리즘의 압축 정도를 정한다

gzip_disable
요청의 User-Agent HTTP 헤더가 지정된 정규식과 일치할 경우 Gzip 압축을 비활성화한다

gzip_http_version
특정 프로토콜 버전에서 Gzip 압축을 활성화한다

gzip_min_length
응답 본문의 길이가 지정된 값보다 작으면 압축을 하지 않는다

gzip_proxied
프록시에서 받은 응답의 본문을 Gzip으로 압축할지 여부를 결정한다

gzip_types
기본 MIME 타입인 text/html 외의 다른 타입에 압축을 활성화한다

gzip_vary
Vary: Accept-Encoding HTTP 헤더를 응답에 추가한다
```



#### SSL 모듈

```
맥락 : http, server

ssl
지정한 서버에 HTTPS를 활성화 한다

ssl_certificate
PEM 인증서의 경로를 정한다

ssl_certificate_key
PEM 비밀 키 파일 경로를 정한다

ssl_client_certificate
클라이언트 PEM 인증서의 경로를 정한다

ssl_crl
엔진엑스에게 인증서의 폐기 상태를 확인할 수 있는 인증서 폐기 목록

ssl_dhparam
디피 헬만 매개변수 파일의 경로를 정한다

ssl_protocols
사용할 프로토콜을 지정한다

ssl_ciphers
사용할 암호화 방식을 지정

ssl_prefer_server_ciphers
서버의 암호화 방식을 클라이언트의 암호화 방식보다 선호할지 여부를 지정

ssl_verify_client
클라이언트에서 보내온 인증서를 검증해서 그 결과를 $ssl_client_verify 변수에 저장하게 한다

ssl_verify_depth
클라이언트 인증 사슬의 검증 깊이를 지정
기본값 : 1

ssl_session_cache
SSL 세션의 캐시를 구성

ssl_session_timeout
SSL 세션이 활성화됐을 경우 이 지시어는 세션 데이터의 제한시간을 정한다
기본 값 : 5m

ssl_password_phrase
비밀 키의 비밀번호를 담고 있는 파일을 지정한다

ssl_buffer_size
SSL을 통해 요청을 제공할 때 사용할 버퍼 크기를 지정한다

ssl_session_tickets
TLS 세션 티켓을 활성화 한다

ssl_session_ticket_key
TLS 세션 티켓을 암/복화화할 때 사용 되는 키 파일의 경로를 설정한다

ssl_trusted_certificate
클라이언트 인증서의 신뢰성을 확인 할 뿐 아니라 OSCP 응답에 스테이플링하는 데도 사용할 신뢰할 수 있는 인증서 파일의 경로를 설정
```



### 5. nginx php 연동

------

- FastCGI
- nginx, php 연동



CGI(Common Gateway Interface)

```
웹 서버와 게이트웨이 애플리케이션(php, python) 간에 정보를 교환할 방법을 기술한 규약
```





FastCGI

```
CGI의 부하가 심해져 비효율적인 해결책을 위해 진화한 CGI
```



uWSGI(Web Server Gateway Interface)

```
uWSGI 모듈은 엔진엑스와 애플리케이션이 uwsgi 프로토콜로 통신하게 해준다
```



SCGI(Simple Common Gateway Interface)

```
CGI 프로토콜의 변종이며 FastCGI와 유사
```



#### 5.1 FastCGI

```
fastcgi_pass
맥락 : location, if
위치에 따라 요청이 FastCGI로 전달되도록 지정하는 지시어

fastcgi_param
맥락 : http, server, location
요청이 FastCGI로 전달되도록 구성하는 지시어
모든 FastCGI 요청에 SCRIPT_FILENAME, QUERY_STRING 두 매개변수가 필수

fastcgi_bind
맥락 : http, server, location
소켓을 기기의 IP 주소에 결속시키는 지시어, FastCGI 통신에 사용하기 원하는 네트워크 인터페이스를 지정할 수 있다

fastcgi_pass_header
맥락 : http, server, location
부가적으로 FastCGI 서버로 전달돼야 할 헤더를 지정하는 지시어

fastcgi_hide_header
맥락 : http, server, location
FastCGI에 숨겨야 하는 헤더를 지정하는 지시어

fastcgi_index
맥락 : http, server, location
FastCGI 서버는 자동 디렉터리 색인을 제공하지 않는다. 요청된 URL가 /로 끝나면 엔진엑스가 fastcgi_index 값을 덧붙인다.

fastcgi_ignore_clinet_abort
문맥 : http, server, location
클라이언트가 웹 서버에 보낸 요청을 취소하면 어떻게 처리할지 정의 할 수 있는 지시어

fastcgi_intercept_errors
맥락 : http, server, location
게이트웨이가 반환한 오류를 엔진엑스가 처리할지, 아니면 클라이언트에 직접 오류 페이지를 반환할지 지정하는 지시어
기본값 : off

fastcgi_read_timeout
맥락 : http, server, location
FastCGI 애플리케이션 응답 제한시간을 정의하는 지시어
기본값 : 60

fastcgi_connect_timeout
문맥 : http, server, location
백엔드 서버 연결 시간제한을 정의하는 지시어
기본값 : 60

fastcgi_send_timeout
맥락 : http, server, location
백엔드 서버에 데이터를 전송하는 시간을 제한한다.

fastcgi_store
맥락 : http, server, location
FastCGI 애플리케이션에서 온 응답을 저장 장치에 파일 형태로 저장하는 단순한 캐시 저장 기능을 활성화

fastcgi_store_access
맥락 : http, server, location
캐시 저장 시 생성되는 파일에 적용될 접근 권한을 정의

fastcgi_temp_path
맥락 : http, server, location
임시 파일과 캐시 저장 파일의 경로를 지정

fastcgi_max_temp_file_size
맥락 : http, server, location
FastCGI 요청에 임시 파일을 사용하지 않게 하려면 이 지시어에 0을 설정하고 아니면 최대 파일 크기를 지정

fastcgi_temp_file_wirte_size
맥락 : http, server, location
임시 파일을 저장 장치에 기록할 때 사용할 버퍼의 크기를 지정하는 지시어

fastcgi_send_lowat
맥락 : http, server, location
TCP 소켓용 SO_SNDLOWAT 플래그를 사용하도록 허용하는 옵션

fastcgi_pass_request_body, fastcgi_pass_request_headers
맥락 : http, server, location
요청 본문과 부가 요청 헤더가 뒷단의 서버에 전달될지 여부를 정하는 지시어
기본값 : on

fastcgi_ignore_headers
맥락 : http, server, location
뒷단 서버가 보낸 응답에서 다음에 나열한 헤더를 엔진엑스가 처리하지 않게 막는 지시어

fastcgi_next_upstream
맥락 : http, server, location
fastcgi_pass가 업스트림 블록과 연결돼 있을 때 이 지시어는 요청을 버리고 해당 블록의 다음 업스트림 서버로 다시 보내야 하는 경우를 정한다

fastcgi_next_upstream timeout
맥락 : http, server, location
fastcgi_next_upstream과 연관돼 사용도리 시간제한 값을 정한다

fastcgi_next_upstream_tries
맥락 : http, server, location
오류 메시지를 반환하기 전에 시도할 최대 업스트림 서버 수를 정의한다

fastcgi_catch_stderr
맥락 : http, server, location
stderr로 보내질 오류 메시지 중 일부를 가로채서 엔진엑스 오류 로그에 저장하게 한다

fastcgi_keep_conn
맥락 : http, server, location
on으로 설정하면 엔진엑스 FastCGI 서버와의 연결을 보존해 부하를 줄인다

fastcgi_socket_keepalive
맥락 : http, server, location
FastCGI 연결이 유지되도록 TCP 소켓을 구성한다

fastcgi_force_ranges
맥락 : http, server, location
on으로 설정하면 엔진엑스는 FastCGI 백엔드에서 오는 응답의 범위를 바이트 단위로 지정하는 기능을 활성화 한다

fastcgi_limit_rate
맥락 : http, server, location
엔진엑스가 FastCGI 백엔드에서 오는 응답을 다운로드하는 속도를 제한한다

fastcgi_cache
맥락 : http, server, location
캐시 구역을 정의하는 지시어
```



#####  5.1.1 FastCGI 캐싱과 버퍼링

엔진엑스를 FastCGI 애플리케이션과 동작하도록 올바르게 구성했다면 캐시 시스템을 설정해 전반적인 서버 성능을 향상시키는 데 도움이 되는 다음 지시어를 선택적으로 사용할 수 있다.

```
fastcgi_cache
맥락 : http, server, location
캐시 영역을 정의하는 지시어

fastcgi_cache_key
맥락 : http, server, location
캐시 키를 정의하는 지시어

fastcgi_cache_method
맥락 : http, server, location
캐시할 HTTP 메서드를 정의하는 지시어

fastcgi_cache_min_uses
맥락 : http, server, location
요청이 캐싱 후보가 되기 전까지의 최소 적중수를 정의하는 지시어

fastcgi_cache_path
맥락 : http
캐시 파일이 저장될 디렉터리를 가르키는 지시어

fastcgi_cache_use_stale
맥락 : http, server, location
특정 상황에서 엔진엑스가 만기된 캐시 데이터라도ㅓ 제곧ㅇ할지 여부를 정의하는 지시어

fastcgi_cache_background_update
맥락 : http, server, location
on으로 설정하면 만기된 캐시 데이터가 제공되는 동안 배후에서 부가 요청을 보내 만기된 캐시 항목을 갱신한다

fastcgi_cache_valid
맥락 : http, server, location
응답 코드마다 별도의 캐시 보관 시간을 지정할 수 있는 지시어

fastcgi_no_cache
맥락 : http, server, location
요청이 특정 조건에 부합할 때 캐시를 적용하지 않아야 할 때가 있다.

fastcgi_cache_bypass
맥락 : http, server, location
캐시에 저장된 응답이 있을 때 응답을 캐시에서 읽어야 할지 알려준다

fastcgi_cache_revalidate
맥락 : http, server, location
활성화 되면 If-modified=since와 If-none=match 헤더로 지시될 때 엔진엑스가 만기된 캐시 항목을 다시 검증한다

fastcgi_buffering, fastcgi_request_buffering
맥락 : http, server, location
뒷단의 FastCGI에서 보낸 응답을 버퍼링할지 말지 결정한다

fastcgi_buffers
맥락 : http, server, location
FastCGI 애플리케이션에서 오는 응답 데이터를 읽는 데 사용도리 버퍼의 용량과 크기를 설정하는 지시어

fastcgi_buffer_size
맥락 : http, server, location
FastCGI 애플리케이션에서 오는 응답의 시작을 읽는데 사용될 버퍼의 크기를 설정하는 지시어

```



#### 5.2 nginx, php 연동

```
php 설치
apt-get install php-fpm

vi /etc/php/7.0/fpm/php.ini
short_open_tag = On

vi /etc/php/7.0/fpm/pool.d/www.conf
user = nginx
group = nginx
listen = /run/php/php7.0-fpm.sock
listen.owner = nginx
listen.group = nginx

설정 후 재시작
systemctl restart php7.0fpm
```



nginx 설정

```
vi /etc/nginx/sites-available/default

index.php 추가

php 추가
location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.0-fpm.sock;
        }   

설정 후 재시작
systemctl reload nginx
```



nginx, php 연동 확인

```
document root : /var/www/html
vi info.php
<?php phpinfo(); ?>
```













### 6. 아파치 엔진엑스 연동

------

- 역프록시
- 아파치 - 엔진엑스 연동



Proxy Server : 클라이언트와 서버 사이에서 데이터를 전달해 주는 서버

#### 6.1 Reverse Proxy

프록시 서버의 일종

특정 서버에 대한 요청이 반드시 경유하도록 설치된 프록시 서버

불특정 다수 사용자의 요청에 응답을 대신함으로써 특정 서버의 부하를 줄이거나, 접속을 제한하여 보안 강화

```
proxy_pass
맥락 : location, if
위치를 알려서 욫어이 뒷단 서버로 전달되도록 지정한다

proxy_method
맥락 : http, server, location
뒷단 서버로 전달될 요청의 HTTP 메서드를 재정의한다

proxy_hide_header
맥락 : http, server, location
기본적으로 엔진엑스는 뒷단 서버에서 받아 클라이언트에게 돌려 줄 응답을 준비하기 때문에 몇가지 헤더를 무시한다.

proxy_pass_header
맥락 : http, server, location
proxy_hide_header와 반대로 이 지시어는 무시되는 헤더를 강제로 클라이언트에 전달되게 한다

proxy_pass_request_bodyproxy_pass_request_headers
맥락 : http, server, location
요청 본문과 부가 요청 헤더가 뒷단 서버로 전달될지 여부를 정한다
기본값 : on

proxy_redirect
맥락 : http, server, location
뒷단 서버에서 유발된 경로 재설정의 Location HTTP 헤더 속 URL을 재작성한다

proxy_next_upstream
맥락 : http, server, location
proxy_pass가 upstream 블록과 연결됐을 때 이 지시어는 요청을 버리고 블록의 다음 업스트림 서버로 재전송하는 경우를 정의한다

proxy_next_upstream_timeout
맥락 : http, server, location
proxy_netx_upstream과 결합해서 사용도리 제한시간을 정한다

proxy_next_upstream_tries
맥락 : http, server, location
오류 메시지를 반환하기 전에 시도할 최대 업스트림 서버 수를 정한다
```



캐시, 버퍼링, 임시 파일

캐시 시스템을 구축할 때 버퍼링 제어 옵션과 엔진엑스가 임시파일을 다루는 방법을 제어하는데 도움을 준다

```
proxy_buffer_size
맥락 : http, server, location
뒷단 서버의 응답 시작 부분을 읽는 데 사용할 버퍼의 크기를 설정한다

proxy_buffering, proxy_request_buffering
맥락 : http, server, location
뒷단 서버에서 오는 응답을 버퍼에 담을지 여부를 정의한다

proxy_buffers
맥락 : http, server, location
뒷단 서버에서 응답 데이터를 읽는 데 사용될 버퍼의 개수와 크기를 설정한다

proxy_busy_buffers_size
맥락 : http, server, location
뒷단에서 받은 데이터가 버퍼에 쌓이다가 지정한 값을 넘으면 그 버퍼는 비워지고 데이터는 클라이언트에 보내진다

proxy_cache
맥락 : http, server, location
캐시 구역을 정의한다

proxy_cache_key
맥락 : http, server, location
캐시 키를 정의한다

proxy_cache_path
맥락 : http
캐시 파일을 저장할 디렉터리와 함께 다른 매개변수를 지정한다

proxy_cache_methods
맥락 : http, server, location
캐시에 맞는 HTTP 메서드를 정한다

proxy_cache_convert_head
맥락 : http, server, location
on이면 캐시되도록 HEAD 메서드를 GET으로 바꾼다

proxy_cache_min_uses
맥락 : http, server, location
요청이 캐시되기에 알맞다고 판단되기 전에 적중될 최소 수치를 정한다

proxy_cache_valid
맥락 : http, server, location
서로 응답 코드 ㅁ유형별로 캐시되는 시간을 바굴 수 있도록 허용한다

proxy_cache_use_stale
맥락 : http, server, location
엔진엑스가 특정 상황에 만기된 캐시 데이터를 사용할지 여부를 정한다

proxy_cache_background_update
맥락 : http, server, location
on으로 설정하면 만기된 캐시 데이터가 제공되는 동안 배후에서 부가 요청을 보내서 만기된 캐시 항목을 갱신한다

proxy_max_temp_file_size
맥락 : http, server, location
0으로 설정하면 프록시 전달에 적합한 요청에 임시 파일을 사용하지 않게 된다

proxy_temp_file_write_size
맥락 : http, server, location
저장 장치에 임시 파일을 저장할 때 쓸 쓰기 작업용 버퍼의 크기를 설정한다

proxy_temp_path
맥락 : http, server, location
임시 파일과 캐시 저장 파일의 경로를 설정한다
```





한계치, 시간 제약, 오류 

시간 제약과 관련된 행동은 물론 뒷단 서버와 통신하는 상황과 관련된 다양한 한계치를 정하는 데 도움이 된다

```
proxy_connect_timeout
맥락 : http, server, location
뒷단 서버에 연결하는 제한시간을 정한다

proxy_read_timeout
맥락 : http, server, location
뒷단 서버에서 데이터를 읽는 제한시간을  정한다

proxy_send_timeout
데이터를 뒷단 서버에 보내는 용도

proxy_ignore_clinet_abort
맥락 : http, server, location
on으로 설정하면 클라이언트가 요청을 취소했더라도 엔진엑스는 프록시 요청을 계속 처리한다
off인 경우에는 엔진엑스도 뒷단 서버로 보내는 요청을 취소한다
기본 값 : off

proxy_intercept_errors
맥락 : http, server, location
on으로 설정하면 오류 코드를 해석하여 error_page 지시어에 지정된 값과 일치하는지 비교할 수 있다.

proxy_send_lowat
맥락 : http, server, location
BSD 기반 운영체제라면 TCP 소켓의 SO_SNDLOWAT 플래그를 쓰게 할 수 있는 옵션

proxy_limit_rate
맥락 : http, server, location
엔진엑스가 뒷단 프록시에서 응답을 다운로드하는 속도를 제한한다
```



SSL 관련 지시어

```
proxy_ssl_certificate
맥락 : http, server, location
SSL 서버의 인증서를 담고 있는 PEM 파일의 경로를 설정한다

proxy_ssl_certificate_key
맥락 : http, server, location
SSL 서버의 인정에 쓰는 보안 키 파일의 경로를 설정한다

proxy_ssl_ciphers
맥락 : http, server, location
뒷단 서버와 SSL 통신을 하는 용도의 암호 알고리즘을 설정한다

proxy_ssl_crl
맥락 : http, server, location
PEM 형식의 인증서 폐기 목록 파일 경로를 설정한다

proxy_ssl_name
맥락 : http, server, location
엔진엑스가 뒷단 서버 SSL 인증서의 폐기 상태를 검증할 때 사용할 서버 이름을 직접 지정한다

proxy_ssl_password_file
맥락 : http, server, location
인증 키를 읽을 때 하나씩 적용해 볼 비밀번호를 보관하는 파일의 경로를 설정

proxy_ssl_server_name
맥락 : http, server, location
on으로 설정하면 서버 이름이 서버명 표시 프로토콜에 따라 뒷단 서버에 알려진다
기본 값 : off

proxy_ssl_session_reuse
맥락 : http, server, location
엔진엑스에게 뒷단 서버와 통신할 때 기존 SSL 세션을 재사용하도록 지시

proxy_ssl_protocols
맥락 : http, server, location
SSL 뒷단 서버와 통신할 때 사용할 프로토콜을 설정

proxy_ssl_trusted_certificate
맥락 : http, server, location
신뢰할 수 있는 인증기관 인증서의 경로를 설정한다

proxy_ssl_verify
맥락 : http, server, location
on으로 설정하면 엔진엑스는 SSL 뒷단 서버의 인증서를 검증한다

proxy_ssl_verify_depth
맥락 : http, server, location
proxy_ssl_verify 지시어가 on으로 설정되면 이 시지어는 인증서 체인의 검증 깊의를 설정한다
```



| 변수 명                     |                                                              |
| --------------------------- | ------------------------------------------------------------ |
| $proxy_host                 | 현 요청에 사용되는 뒷단 서버의 호스트명을 가진다             |
| $proxy_port                 | 현 요청에 사용되는 뒷단 서버의 포트 번호를 가진다            |
| $proxy_add_x_forwarde_for   | X-Forwarded-For 요청 헤더 값과 클라이언트의 원격 주소를 가진다 |
| $proxy_internal_body_length | (proxy_set_body 지시어로 요청이 된)요청 본문의 길이          |



#### 6.2 아파치 - 엔진엑스 연동

```
apache 설치
apt-get install apache2

port 변경
vi /etc/apache2/ports.conf
port 8080

연동 확인을 위해 localhost외에는 접근 불가 설정
vi /etc/apache2/sites-avaolable/000-default.conf
<VirtualHost *:8080>
        ServerName test1.co.kr:8080
        ServerAlias www.test1.co.kr
         DocumentRoot /var/www/html
        <Directory /var/www >
        Options Indexes FollowSymLinks
        AllowOverride None
        Order deny,allow
        allow from 127.0.0.1
        deny from all
        </Directory>
 </VirtualHost>
 
 
 nginx proxy 설정
 /etc/nginx/sites-available/default
 proxy_pass http://127.0.0.1:8080;
 
 systemctl reload nginx
```



예제 : reverse proxy, vhost

nginx : 80 apache : 8080 tomcat : 8888

한 서버에 nginx, apache, tomcat을 띄우고 nginx를 앞단에 놓아 reverse proxy를 통해 apache와 tomcat 연동

nginx, apache는 도메인 한개씩 tomcat은 vhost를 통해 두개의 도메인 사용



```
테스트를 위해 local hosts 파일에 도메인 등록
172.16.120.20 nginx.com apache.com tomcat1.com tomcat2.com
```

































