# Linux(rpm, yum, apt) - 설치 패키지

| 작성일     | 작성자 | 작성내용           | 비고 |
| ---------- | ------ | ------------------ | ---- |
| 2020.03.10 | 박성민 | 최초문서 작성(rpm) |      |



## rpm

### 1. 주요 명령어와 옵션

Redhat Package Manager

레드햇에서 프로그램 설치와 업그레이드 및 삭제 등을 편리하게 하기위해 패키지 형태의 바이너리로 배포

#### 

| 명령어 | 설명                                                         |
| ------ | ------------------------------------------------------------ |
| i      | 새로운 패키지를 설치할 때 사용 ( --install)                  |
| U      | 기존의 패키지를 새로운 버전의 패키지로 업그레이드할 때 사용하고 설치된 패키지가 없을 경우 패키지를 설치한다 |
| F      | 이전 버전이 설치되어 있는 경우에만 설치한다 (-- freshen)     |
| e      | 설치 된 패키지 삭제한다                                      |
| v      | 메시지를 자세히 보여준다                                     |
| h      | 진행 상황을 '#' 기호로 표시한다                              |
| q      | 패키지가 설치 되어있는지 확인하고 있으면 이름과 버전 출력한다 |
| qa     | 설치된 모든 패키지를 보여준다                                |



#### 가능한 옵션



##### --Nodeps

rpm 은 기본적으로 의존성을 확인하므로 의존성 있는 패키지가 설치되지 않았을 경우 설치나 업그레이드가 안 될수 있다. --nodeps 옵션을 지정하면 의존성을 확인하지 않으므로 통과하게 된다.

##### --Replacepkgs

패지키가 이미 설치되어 있으면 rpm 은 설치를 거부하나 이 옵션을 추가하면 설치를 진행한다.

##### --Replacefiles

설치하려는 패키지가 기존에 설치된 패키지의 파일을 교체하는 경우 rpm 은 설치를 거부하나 이 옵션을 추가하면 설치를 진행한다.

##### --Oldpackage

업그레이드 옵션(-U) 으로 패키지 설치시 설치하려는 버전이 기존에 설치된 버전보다 낮으면 설치를 진행하지 않는다. --oldpackage 옵션을 사용하면 버전이 낮아도 설치되므로 패키지 downgrade 시 유용하다.

##### --Force

위에서 설명한 --**replacepkgs**, --**replacefiles**, 그리고 --**oldpackage** 세 개 옵션을 사용한 것과 동일하다. 패키지 다운그레이드나 강제 재설치등에 사용할 수 있으나 기존 파일을 덮어쓰므로 주의해야 한다.



### 2. apache, php, php-fpm 설치 및 패키지 옵션 정리

#### apache 설치

##### 설치 

```
rpm -ivh 패키지명

apache 설치
wget https://rpmfind.net/linux/centos/6.10/os/x86_64/Packages/httpd-2.2.15-69.el6.centos.x86_64.rpm
rpm -ivh httpd-2.2.15-69.el6.centos.x86_64.rpm

의존성 문제로 httpd-tools 설치
wget https://rpmfind.net/linux/centos/6.10/os/x86_64/Packages/httpd-tools-2.2.15-69.el6.centos.x86_64.rpm
rpm -ivh httpd-tools-2.2.15-69.el6.centos.x86_64.rpm

```



##### 설치 목록 확인

```
rpm -qa | grep 패키지명

[root@localhost SOURCES]# rpm -qa | grep httpd
httpd-tools-2.2.15-69.el6.centos.x86_64
httpd-2.2.15-69.el6.centos.x86_64
```



##### 설치 경로 확인

```
rpm -ql httpd
```



##### 설정 파일 목록 보기

```
rpm -qc 

[root@localhost SOURCES]# rpm -qc httpd
/etc/httpd/conf.d/welcome.conf
/etc/httpd/conf/httpd.conf
/etc/httpd/conf/magic
/etc/logrotate.d/httpd
/etc/sysconfig/htcacheclean
/etc/sysconfig/httpd
/var/www/error/HTTP_BAD_GATEWAY.html.var
/var/www/error/HTTP_BAD_REQUEST.html.var
/var/www/error/HTTP_FORBIDDEN.html.var
/var/www/error/HTTP_GONE.html.var
/var/www/error/HTTP_INTERNAL_SERVER_ERROR.html.var
/var/www/error/HTTP_LENGTH_REQUIRED.html.var
/var/www/error/HTTP_METHOD_NOT_ALLOWED.html.var
/var/www/error/HTTP_NOT_FOUND.html.var
/var/www/error/HTTP_NOT_IMPLEMENTED.html.var
/var/www/error/HTTP_PRECONDITION_FAILED.html.var
/var/www/error/HTTP_REQUEST_ENTITY_TOO_LARGE.html.var
/var/www/error/HTTP_REQUEST_TIME_OUT.html.var
/var/www/error/HTTP_REQUEST_URI_TOO_LARGE.html.var
/var/www/error/HTTP_SERVICE_UNAVAILABLE.html.var
/var/www/error/HTTP_UNAUTHORIZED.html.var
/var/www/error/HTTP_UNSUPPORTED_MEDIA_TYPE.html.var
/var/www/error/HTTP_VARIANT_ALSO_VARIES.html.var
/var/www/error/contact.html.var
/var/www/error/include/bottom.html
/var/www/error/include/spacer.html
/var/www/error/include/top.html
```



##### 제거

```
rpm -ev 패키지명

apache 삭제
rpm -e --nodeps httpd-2.2.15-69.el6.centos.x86_64
```



##### 업그레이드

```
rpm -Uvh 패키지명
```



##### 설치용량 확인

```
rpm -qa --queryformat '%{NAME} %{SIZE} \n' 패키지명

[root@localhost SOURCES]# rpm -qa --queryformat '%{NAME} %{SIZE} \n' httpd
httpd 3170514 

[root@localhost SOURCES]# rpm -qi httpd | grep ^Size | awk '{print $3}'                  
3170514
```



##### 파일이 속한 패키지 찾기

```
rpm -qf 

[root@localhost SOURCES]# which httpd
/usr/sbin/httpd
[root@localhost SOURCES]# rpm -qf /usr/sbin/httpd
httpd-2.2.15-69.el6.centos.x86_64
```



##### 패키지의 의존성 목록 보기

```
rpm -qR 

[root@localhost SOURCES]# rpm -qR httpd
/bin/bash  
/bin/sh  
/bin/sh  
/bin/sh  
/bin/sh  
/bin/sh  
/etc/mime.types  
/usr/sbin/useradd  
apr-util-ldap  
chkconfig  
config(httpd) = 2.2.15-69.el6.centos
httpd-tools = 2.2.15-69.el6.centos
initscripts >= 8.36
libapr-1.so.0()(64bit)  
libaprutil-1.so.0()(64bit)  
libc.so.6()(64bit)  
libc.so.6(GLIBC_2.2.5)(64bit)  
libc.so.6(GLIBC_2.3)(64bit)  
libc.so.6(GLIBC_2.3.4)(64bit)  
libc.so.6(GLIBC_2.4)(64bit)  
libcrypt.so.1()(64bit)  
libdb-4.7.so()(64bit)  
libexpat.so.1()(64bit)  
liblber-2.4.so.2()(64bit)  
libldap-2.4.so.2()(64bit)  
libm.so.6()(64bit)  
libpcre.so.0()(64bit)  
libpthread.so.0()(64bit)  
libpthread.so.0(GLIBC_2.2.5)(64bit)  
libselinux.so.1()(64bit)  
libz.so.1()(64bit)  
rpmlib(CompressedFileNames) <= 3.0.4-1
rpmlib(FileDigests) <= 4.6.0-1
rpmlib(PayloadFilesHavePrefix) <= 4.0-1
rpmlib(VersionedDependencies) <= 3.0.3-1
rtld(GNU_HASH)  
system-logos >= 7.92.1-1
rpmlib(PayloadIsXz) <= 5.2-1
```



##### 자세한 정보 보기

```
rpm -qi httpd

[root@localhost SOURCES]# rpm -qi httpd
Name        : httpd                        Relocations: (not relocatable)
Version     : 2.2.15                            Vendor: CentOS
Release     : 69.el6.centos                 Build Date: 
Install Date:                                  Build Host: x86-01.bsys.centos.org
Group       : System Environment/Daemons    Source RPM: httpd-2.2.15-69.el6.centos.src.rpm
Size        : 3170514                          License: ASL 2.0
Signature   : RSA/SHA1, 2018년 06월 20일 (수) 오후 08시 36분 47초, Key ID 0946fca2c105b9de
Packager    : CentOS BuildSystem <http://bugs.centos.org>
URL         : http://httpd.apache.org/
Summary     : Apache HTTP Server
Description :
The Apache HTTP Server is a powerful, efficient, and extensible
web server.
```





#### PHP 설치

```
remi-release 설치여부 확인
rpm -qa | grep remi-release

epel-release 설치(의존성 문제 해결)
rpm -ivh http://www.atblog.co.kr/file/package/epel-release-6-8.noarch.rpm

remi-release 설치
rpm -ivh http://www.atblog.co.kr/file/package/remi-release-6.rpm

[root@localhost SOURCES]# rpm -qa | grep remi-release-6.5-1.el6.remi.noarch
remi-release-6.5-1.el6.remi.noarch


wget http://www.rpmfind.info/linux/remi/enterprise/7/remi/x86_64/php55-php-devel-5.5.38-12.el7.remi.x86_64.rpm

의존성 다운로드 필요
[root@localhost SOURCES]# rpm -ivh php55-php-devel-5.5.38-12.el7.remi.x86_64.rpm
경고: php55-php-devel-5.5.38-12.el7.remi.x86_64.rpm: Header V4 DSA/SHA1 Signature, key ID 00f97f56: NOKEY
오류: Failed dependencies:
        php55-php-cli(x86-64) = 5.5.38-12.el7.remi is needed by php55-php-devel-5.5.38-12.el7.remi.x86_64
        autoconf is needed by php55-php-devel-5.5.38-12.el7.remi.x86_64
        automake is needed by php55-php-devel-5.5.38-12.el7.remi.x86_64
        pcre-devel(x86-64) >= 8.20 is needed by php55-php-devel-5.5.38-12.el7.remi.x86_64
        php55-php-pecl-jsonc-devel(x86-64) is needed by php55-php-devel-5.5.38-12.el7.remi.x86_64


wget https://rpmfind.net/linux/remi/enterprise/7/remi/x86_64/php55-php-cli-5.5.38-12.el7.remi.x86_64.rpm

[root@localhost SOURCES]# rpm -ivh php55-php-cli-5.5.38-12.el7.remi.x86_64.rpm 
경고: php55-php-cli-5.5.38-12.el7.remi.x86_64.rpm: Header V4 DSA/SHA1 Signature, key ID 00f97f56: NOKEY
오류: Failed dependencies:
        php55-php-common(x86-64) = 5.5.38-12.el7.remi is needed by php55-php-cli-5.5.38-12.el7.remi.x86_64
        libcrypto.so.10(OPENSSL_1.0.2)(64bit) is needed by php55-php-cli-5.5.38-12.el7.remi.x86_64
        libc.so.6(GLIBC_2.14)(64bit) is needed by php55-php-cli-5.5.38-12.el7.remi.x86_64
        libc.so.6(GLIBC_2.15)(64bit) is needed by php55-php-cli-5.5.38-12.el7.remi.x86_64
        libpcre.so.1()(64bit) is needed by php55-php-cli-5.5.38-12.el7.remi.x86_64
        
        
        
        
        
        
        
        
        
        
        
        
        

```



##### mysql 설치

```




mysql-community-client-8.0.19-1.el6.x86_64
mysql-community-common-8.0.19-1.el6.x86_64
mysql-community-libs-compat-8.0.19-1.el6.x86_64
mysql-community-server-8.0.19-1.el6.x86_64
mysql-community-libs-8.0.19-1.el6.x86_64
```



## yum

### 1.주요 명령어와 옵션

| 명령어                    | 설명                                                       | 비고 |
| ------------------------- | ---------------------------------------------------------- | ---- |
| yum check-update          | 현재 인스톨된 프로그램 중에 업데이트 된 것을 체크해줍니다. |      |
| yum clean all             | 캐시 되어 있는 것을 모두 지웁니다.                         |      |
| yum deplist               | yum 패키지에 대한 의존성 테스트합니다.                     |      |
| yum downgrade 패키지      | yum을 통한 패키지 다운그레이드합니다.                      |      |
| yum erase 패키지          | yum을 통한 시스템에서 삭제합니다.                          |      |
| yum groupinfo 그룹        | 그룹패키지의 정보를 보여줍니다.                            |      |
| yum groupinstall 그룹     | 그룹패키지를 설치합니다.                                   |      |
| yum grouplist 그룹        | 그룹리스트에 관한 정보를 확인합니다.                       |      |
| yum groupremove 그룹      | 그룹리스트에 관해 삭제합니다.                              |      |
| yum help                  | yum의 도움말을 확인합니다.                                 |      |
| yum info 그룹 또는 패키지 | 패키지 또는 그룹의 패키지를 자세하게 확인합니다.           |      |
| yum install 패키지        | 시스템으로 패키지의 Install 을 실시합니다.                 |      |
| yum list                  | 서버에 있는 그룹 및 패키지의 리스트를 보여줍니다.          |      |
| yum localinstall          | 로컬에 설치합니다.                                         |      |
| yum makecache             | 캐쉬를 다시 올립니다.                                      |      |
| yum provides FilePath명   | 파일이 제공하는 패키지 정보 출력합니다.                    |      |
| yum reinstall             | 패키지를 재인스톨 합니다.                                  |      |
| yum update 패키지         | 패키지를 업데이트합니다.                                   |      |
| yum upgrade 패키지        | 패키지를 업그레이드 합니다.                                |      |
| yum search 키워           | 키워드로 시작하는 패키지를 검색할수 있습니다.              |      |

### 옵션

| 옵션                                         | 설명                                                         | 비고 |
| -------------------------------------------- | ------------------------------------------------------------ | ---- |
| -h, --help                                   | 해당 명령어의 도움말을 보여주고 실행이 종료됩니다.           |      |
| -t, --tolerant                               | 에러를 자동으로 잡아서 설치합니다.                           |      |
| -C, --cacheonly                              | 캐시를 업데이트 하지 않고 전체 시스템 캐시 실행합니다.       |      |
| -c [config file], --config=[config file]     | 파일 위치를 알려줍니다.                                      |      |
| -R [minutes], --randomwait=[minutes]         | 최대치의 명령어 실행시 기다립니다.                           |      |
| -d [debug level], --debuglevel=[debug level] | 최종 결과를 디버깅합니다.                                    |      |
| --showduplicates                             | 중복요소를 보여줍니다.                                       |      |
| -e [error level], --errorlevel=[error level] | 결과 중 에러를 보여줍니다.                                   |      |
| --rpmverbosity=[debug level name]            | rpm에서 결과물을 디버깅합니다.                               |      |
| --version                                    | Yum 버전을 보여주고 실행이 종료됩니다.                       |      |
| -y, --assumeyes                              | 모든 물음에 예를 진행합니다.                                 |      |
| -q, --quiet                                  | 모든 작업이 종료됩니다.                                      |      |
| -v, --verbose                                | 작업을 장황하게 합니다.                                      |      |
| --installroot=[path]                         | root권한으로 path위치에 인스톨을 진행합니다.                 |      |
| --enablerepo=[repo]                          | 1개 이상의 저장소 위치에 저장시킵니다.                       |      |
| --disablerepo=[repo]                         | 1개 이상의 저장소 위치에 저장시키지 않습니다.                |      |
| -x [package], --exclude=[package]            | 패키지 이름을 제외시킵니다.                                  |      |
| --disableexcludes=[repo]                     | 이름으로 플러그인을 설치를 중단합니다.                       |      |
| --obsoletes                                  | 오래된 패키지는 업데이트를 하는 동안 적절히 삭제 및 교체됩니다. |      |
| --noplugins                                  | yum plugin이 없도록 합니다.                                  |      |
| --nogpgcheck                                 | gpg signature를 불가능하게 합니다.                           |      |
| --skip-broken                                | 문제 있는 패키지는 자동으로 스킵해서 넘어갑니다.             |      |
| --color=COLOR                                | 컬러가 사용되었을 때 조정합니다.                             |      |
| --releasever=RELEASEVER                      | $releasever의 값을 yum config와 repo파일에서 조정합니다.     |      |
| --setopt=SETOPTS                             | 임의로 config와 repo 옵션값을 지정합니다.                    |      |
| --disablepresto                              | Presto 플러그인을 중단하고 deltarpm을 다운로드 받지 않습니다. |      |



### 2. apache, php, mysql 설치 및 패키지 옵션 정리

```
[root@localhost bizspring]# yum list httpd
Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
 * base: mirror.navercorp.com
 * epel: ftp.jaist.ac.jp
 * extras: mirror.navercorp.com
 * remi-php72: ftp.riken.jp
 * remi-safe: ftp.riken.jp
 * updates: mirror.navercorp.com
Installed Packages
httpd.x86_64                                             2.2.15-69.el6.centos                                              installed
[root@localhost bizspring]# yum list mysql-server
Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
 * base: mirror.navercorp.com
 * epel: ftp.jaist.ac.jp
 * extras: mirror.navercorp.com
 * remi-php72: ftp.riken.jp
 * remi-safe: ftp.riken.jp
 * updates: mirror.navercorp.com
Available Packages
mysql-server.x86_64                                               5.1.73-8.el6_8                                                base
[root@localhost bizspring]# yum list php
Loaded plugins: fastestmirror, refresh-packagekit, security
Loading mirror speeds from cached hostfile
 * base: mirror.navercorp.com
 * epel: ftp.jaist.ac.jp
 * extras: mirror.navercorp.com
 * remi-php72: ftp.riken.jp
 * remi-safe: ftp.riken.jp
 * updates: mirror.navercorp.com
Available Packages
php.x86_64                                               7.2.29-1.el7.remi                                                remi-php72

http - 2.2.15
mysql - 5.1.73
php - 7.2.29 설치 가능
```



#### 설치

```
yum install httpd
yum install php php-mbstring php-pdo php-xml php-mysql
yum install mysql mysql-server
```

#### 서비스 시작

```
service httpd start
service mysqld start
```

#### 서비스 버전 확인

```
[root@localhost ~]# httpd -v
Server version: Apache/2.2.15 (Unix)
Server built:   Jun 19 2018 15:45:13

[root@localhost ~]# mysql -v
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.1.73 Source distribution
```

![1585636777497](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1585636777497.png)



#### php 연동 확인

```
cd /var/www/html
vi testinfo.php 생성
<?php
	phpinfo();
?>
```

![1585636898103](C:\Users\minsoo\AppData\Roaming\Typora\typora-user-images\1585636898103.png)



































