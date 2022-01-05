# MySQL Replication



#### MySQL Replication란?

```
리플리케이션(Replication)은 복제를 뜻하며 2대 이상의 DBMS를 나눠서 데이터를 저장하는 방식이며, 사용하기 위한 최소 구성은 Master / Slave 구성을 하여야 됩니다.
```



##### Master DBMS 역할

```
웹서버로 부터 데이터 등록/수정/삭제 요청시 바이너리로그(Binarylog)를 생성하여 Slave 서버로 전달하게 됩니다
(웹서버로 부터 요청한 데이터 등록/수정/삭제 기능을 하는 DBMS로 많이 사용됩니다)
```



##### Slave DBMS 역할 : 

```
Master DBMS로 부터 전달받은 바이너리로그(Binarylog)를 데이터로 반영하게 됩니다
(웹서버로 부터 요청을 통해 데이터를 불러오는 DBMS로 많이 사용됩니다)
```



#### MySQL Replication 사용목적

##### 1. 데이터 백업

##### 2. DBMS의 부하분산

#### Mysql Replication 동작 원리

```
MySQL 의 Replication 은 기본적으로 비동기 복제 방식을 사용하고 있다.
Master 노드에서 변경되는 데이터에 대한 이력을 로그(Binary Log)에 기록하면, Replication Master Thread 가 (비동기적으로) 이를 읽어서 Slave 쪽으로 전송하는 방식이다.

MySQL 에서 Replication 을 위해 반드시 필요한 요소는 다음과 같다.

- Master 에서의 변경을 기록하기 위한 Binary Log
- Binary Log 를 읽어서 Slave 쪽으로 데이터를 전송하기 위한 Master Thread
- Slave 에서 데이터를 수신하여 Relay Log 에 기록하기 위한 I/O Thread
- Relay Log 를 읽어서 해당 데이터를 Slave 에 Apply(적용)하기 위한 SQL Thread
```



```
1. 클라이언트(Application)에서 Commit 을 수행한다.
2. Connection Thead 는 스토리지 엔진에게 해당 트랜잭션에 대한 Prepare(Commit 준비)를 수행한다.
3. Commit 을 수행하기 전에 먼저 Binary Log 에 변경사항을 기록한다.
4. 스토리지 엔진에게 트랜잭션 Commit 을 수행한다.
5. Master Thread 는 시간에 구애받지 않고(비동기적으로) Binary Log 를 읽어서 Slave 로 전송한다.
6. Slave 의 I/O Thread 는 Master 로부터 수신한 변경 데이터를 Relay Log 에 기록한다. (기록하는 방식7. 은 Master 의 Binary Log 와 동일하다)
8. Slave 의 SQL Thread 는 Relay Log 에 기록된 변경 데이터를 읽어서 스토리지 엔진에 적용한다.
```



##### Master Thread

```
MySQL Replication 에서는 Slave Thread 가 Client 이고 Master Thread 가 Server 이다. 즉, Slave Thread 가 Master Thread 쪽으로 접속을 요청하기 때문에 Master 에는 Slaver Thread 가 로그인할 수 있는 계정과 권한(REPLICATION_SLAVE)이 필요하다

Master 쪽으로 동시에 다수의 Slave Thread 가 접속할 수 있으므로 Slave Thread 당 하나의 Master Thread 가 대응되어 생성된다. Master Thread 는 한가지 역할만을 수행하는데, 이는 Binary Log 를 읽어서 Slave 로 전송하는 것이다. 이 때문에 Binlog Sender 또는 Binlog Dump 라고도 불린다.
```



##### Slave I/O Thread

```
Slave I/O Thread 는 Master 로부터 연속적으로 수신한 데이터를 Relay Log 라는 로그 파일에 순차적으로 기록한다. Relay Log 파일의 Format 은 Master 측의 Binary Log Format 과 정확하게 일치한다. 인덱스 파일도 똑같이 존재하고 파일 명에 6 자리 숫자가 붙는 것도 동일하다.
```



##### Slave SQL Thread

```
Slave SQL Thread 는 Relay Log 에 기록된 변경 데이터 내용을 읽어서 스토리지 엔진을 통해 Slave 측에 Replay(재생)하는 Thread 이다
```



#### MySQL Replication 구조

```
1. Master-slave

2. Master-Master

3. Master-slave,slave(1:N)

4. Master-Master-slave(N:1)

5. Master Master Master(순환형)
```



##### replication 사전 작업

```
## 계정생성(기본 계정이있다면 생략)
create user 계정@'%' identified by '패스워드';

## mysql slave 권한 추가
grant all privileges on repl_db.* to 계정명@'%' identified by '패스워드';
flush privlieges
```



##### 서버 연결

```mysql
mysql> change master to
master_host='192.168.65.148',
master_user='repl_user',
master_password='test456',
master_log_file='mysql-bin.000010',
master_log_pos=1487;

MASTER_HOST : Mster 서버 IP 입력
MASTER_USER : 리플리케이션 ID
MASTER_PASSWORD : 리플리케이션 PW
MASTER_LOG_FILE : MASTER STATUS 로그파일명
MASTER_LOG_POS : MASTER STATUS에서 position 값
```



##### 서버 설정

```
## 서버 설정은 my.cnf 에 진행하며
하드코딩으로 master정보를 지정해도 되지만 생략가능
생략할시 sql문으로 추가 진행

replicate-do-db : 복제하고자 하는 데이터베이스를 의미하며 2개이상의 데이터베이스를 할경우 replicate-do-db를 추가하시면 됩니다
master-host : Master 서버의 IP를 입력
master-user : Master 서버에 생성한 리플리케이션(Replication) ID 입력
master-password : Master 서버에 생성한 리플리케이션(Replication) PW 입력
master-port : MySQL에서 사용하는 포트 입력
Server-id : Master 서버의 server-id를 제외하고 1~(2^32)-1내의 숫자로 설정하시면 됩니다
```



##### replication 확인

```mysql
## Master
mysql> show master status;
+------------------+----------+--------------+------------------+
| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |
+------------------+----------+--------------+------------------+
| mysql-bin.000001 |     1845 | TEST_IDR1    |                  |
+------------------+----------+--------------+------------------+

## slave
mysql> show slave status\G;
*************************** 1. row ***************************
               Slave_IO_State: Waiting for master to send event
                  Master_Host: 172.16.44.101
                  Master_User: 2n9soft
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql-bin.000001
          Read_Master_Log_Pos: 1845
               Relay_Log_File: mysqld-relay-bin.000742
                Relay_Log_Pos: 530
        Relay_Master_Log_File: mysql-bin.000001
             Slave_IO_Running: Yes
            Slave_SQL_Running: Yes
              Replicate_Do_DB: TEST_IDR1
          Replicate_Ignore_DB: 
           Replicate_Do_Table: 
       Replicate_Ignore_Table: 
      Replicate_Wild_Do_Table: TEST_IDR1.%
  Replicate_Wild_Ignore_Table: 
                   Last_Errno: 0
                   Last_Error: 
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 1845
              Relay_Log_Space: 831
              Until_Condition: None
               Until_Log_File: 
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File: 
           Master_SSL_CA_Path: 
              Master_SSL_Cert: 
            Master_SSL_Cipher: 
               Master_SSL_Key: 
        Seconds_Behind_Master: 0
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 0
                Last_IO_Error: 
               Last_SQL_Errno: 0
               Last_SQL_Error: 
```



```
Slave_IO_State : Master서버의 연결을 시도하고 Master서버로 부터 이벤트를 기다리며, 재연결하는지에 대해 알려줍니다
Master_Host : 연결된 Master서버 호스트 입니다
Master_User : Master서버 연결하는데 사용되는 사용자 입니다
Master_Port : Master서버 연결하는데 사용되는 포트 입니다
Connect_Retry : --master-connect-retry 옵션의 현재 값 입니다
Master_Log_File : I/O 쓰레드에서 현재 읽고 있는 바이너리 로그파일 이름 입니다
Read_Master_Log_Pos : I/O 쓰레드에서 현재 Master 서버의 바이너리 로그에서 읽은 곳가지의 위치 입니다
Relay_Log_File : SQL 쓰레드에서 현재 relay 로그파일 이름 입니다
Relay_Log_Pos : SQL 쓰레드에 의해 Relay 로그에서 읽고 실행한 곳까지의 위치 입니다
Relay_Master_Log_File : SQL 스레드에 의해 실행된 최근 Master서버의 바이너리 로그 파일의 이름입니다
Slave_IO_Running : I/O 쓰레드가 시작되어 Master서버의 성공적으로 연결되어있는지 여부 여부 입니다
Slave_SQL_Running : SQL 쓰레드가 시작되었는지의 여부 입니다
Replicate_Do_DB : Master서버에서 업데이트된 데이터를 반영될 DB 입니다
Last_Errno : 가장 최근에 사용된 쿼리의 에러메시지의 번호로 리턴됩니다
Last_Error : 가장 최근에 사용된 쿼리의 에러메시지의 번호로 리턴됩니다
Exec_Master_Log_Pos : Master서버의 바이너리 로그의 Relay_Master_Log_File로 부터 SQL쓰레드의 의해 마지막 이벤트의 위치 입니다
Relay_Log_Space : 존재하는 모든 Relay 로구우ㅏ 전체 사이즈 입니다
Master_SSL_Allowed : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 입니다
Master_SSL_CA_File : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 입니다
Master_SSL_CA_Path : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 입니다
Master_SSL_Cert : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 입니다
Master_SSL_Cipher : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 입니다
Master_SSL_Key : Master서버에 연결하기 위해 Slave에 의해 사용된 SSL 파라미터 
Seconds_Behind_Master : Master서버에서 실행된 이벤트의 타임스탬프 이후 경과된 시간(초 단위)의 수 입니다
```



##### 1. Master-slave

```
Master : 172.16.44.101
slave : 172.16.44.102
```

##### 설정

```mysql
## Master replication
server-id      = 1
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1
log_bin_trust_function_creators=1
```

```mysql
## slave replication
server-id = 2
replicate-wild-do-table=TEST_IDR1.%
replicate-do_db = TEST_IDR1
```



##### 2. master-master

```
Master1 : 172.16.44.101
Master2 : 172.16.44.102
```

##### 설정

```mysql
# master replication
server-id      = 1
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# master replication
server-id = 2
log-bin = mysql-bin
binlog-do_db = TEST_IDR1
```

##### replication 설정

```mysql
## master1
reset master
stop slave
reset slave

## master2
reset master
stop slave
reset slave

## master1
start slave

## master2
start slave
```



##### 3. master-master-master

```
Master1 : 172.16.44.101
Master2 : 172.16.44.102
Master3 : 172.16.44.103
```

##### 설정

```mysql
# master replication
server-id      = 1
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# master replication
server-id      = 2
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# master replication
server-id      = 3
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1
```

##### replication 설정

```mysql
## master1
reset master
stop slave
reset slave

## master2
reset master
stop slave
reset slave

## master3
reset master
stop slave
reset slave

## master1
CHANGE MASTER TO
MASTER_HOST='172.16.44.103',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft';
start slave

## master2
CHANGE MASTER TO
MASTER_HOST='172.16.44.101',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft';
start slave

## master3
CHANGE MASTER TO
MASTER_HOST='172.16.44.102',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft';
start slave
```



##### 4. 1:N (master: 1 slave : N)

```
Master : 172.16.44.101
slave1 : 172.16.44.102
slave2 : 172.16.44.103
```

##### 설정

```mysql
# master replication
server-id      = 1
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# slave1 replication
server-id      = 2
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# slave2 replication
server-id      = 3
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1
```

##### replication 설정

```mysql
## master1
reset master

## slave1
stop slave
reset slave

## slave2
stop slave
reset slave

## slave1
CHANGE MASTER TO
MASTER_HOST='172.16.44.101',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft';
start slave

## slave2
CHANGE MASTER TO
MASTER_HOST='172.16.44.101',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft';
start slave
```



##### 5. N:1 (master: N slave : 1)



- mysql 5.7 이상 지원

```
Master1 : 172.16.44.101
Master2 : 172.16.44.102
slave : 172.16.44.103
```

##### 설정

```mysql
# master replication
server-id      = 1
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# slave1 replication
server-id      = 2
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1

# slave2 replication
server-id      = 3
log-bin        = mysql-bin
binlog-do-db = TEST_IDR1
```

##### replication 설정

```mysql
## master1
reset master

## master2
reset master

## slave
stop slave
reset slave

CHANGE MASTER TO
MASTER_HOST='172.16.44.101',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft',
FOR CHANNEL 'master_1';

CHANGE MASTER TO
MASTER_HOST='172.16.44.102',
MASTER_USER='2n9soft',
MASTER_PASSWORD='2n9soft',
FOR CHANNEL 'master_2';

START SLAVE FOR CHANNEL 'master_1';
START SLAVE FOR CHANNEL 'master_2';

show slave status for channel 'master_1'\G;
show slave status for channel 'master_2'\G;

master 마다 각각 다른 relay-log file을 저장
```





















