# Linux 

#### 1. rpm

Redhat Package Manager

레드햇에서 프로그램 설치와 업그레이드 및 삭제 등을 편리하게 하기위해 패키지 형태의 바이너리로 배포

| 옵션 | 설명                                                         |
| ---- | ------------------------------------------------------------ |
| i    | 새로운 패키지를 설치할 때 사용 ( --install)                  |
| U    | 기존의 패키지를 새로운 버전의 패키지로 업그레이드할 때 사용하고 설치된 패키지가 없을 경우 패키지를 설치한다 |
| F    | 이전 버전이 설치되어 있는 경우에만 설치한다 (-- freshen)     |
| e    | 설치 된 패키지 삭제한다                                      |
| v    | 메시지를 자세히 보여준다                                     |
| h    | 진행 상황ㅇ르 '#' 기호로 표시한다                            |
| q    | 패키지가 설치 되어있는지 확인하고 있으면 이름과 버전 출력한다 |
| qa   | 설치된 모든 패키지를 보여준다                                |



#### 2. yum

Yellowdog Update Manager 의 약어로 RPM의 단점인 의존성 문제를 해결하기 위해 제공되는 것



```
yum (옵션) (명령 패키지명)
```



| 옵션 | 설명                               |
| ---- | ---------------------------------- |
| h    | 도움말을 출력한다                  |
| y    | 설치 과정 모든 질문에 yes로 답한다 |
| v    | 자세한 메시지를 출력한다           |



| 명령         | 설명                                                         |
| ------------ | ------------------------------------------------------------ |
| install      | 패키지를 설치한다                                            |
| update       | 패키지명이 없으면 전체 업데이트 있으면 해당 패키지만 업데이트 |
| check-update | 현재 시스템에 설치된 패키지를 기준으로 업데이트 목록을 출력한다 |
| remove       | 설치된 패키지를 삭제한다                                     |
| list         | 패키지 목록을 확인한다                                       |
| info         | 패키지 정보를 확인한다                                       |



#### 3. apt-get



```
apt-get [옵션] 명령
```



| 옵션 | 설명                                                      |
| ---- | --------------------------------------------------------- |
| h    | 도움말                                                    |
| q    | 기록할 수 있는 출력                                       |
| qq   | 올 이외의 메시지 표시하지 않기                            |
| d    | 압축 파일을 설치하거나 압축 해제하지 않고 다운로드만 하기 |
| s    | 동작 없음. 명령 시뮬레이션 실행                           |
| y    | 모든 질문을 표시하지 않고 예라고 대답                     |
| f    | 망가진 의존성 패키지가 있는 시스템을 즉시 정정하려 합니다 |
| m    | 압축 파일을 찾을 수 없어도 계속 진행하도록 합니다         |
| u    | 업그레이드한 패키지의 목록도 표시합니다                   |
| b    | 소스 패키지를 가져온 후 빌드합니다                        |
| V    | 자세한 버전 번호 표시                                     |
| c    | 지정한 설정 파일 읽기                                     |
| o    | 임의의 옵션을 설정                                        |
|      |                                                           |



| Command         | 설명                                                |
| --------------- | --------------------------------------------------- |
| update          | 새 패키지 목록 가져오기                             |
| upgrade         | 업그레이드 실행                                     |
| install         | 새 패키지 설치                                      |
| remove          | 패키지 제거                                         |
| autoremove      | 사용하지 않는 모든 패키지를 자동으로 제거           |
| purge           | 패키지와 설정 파일을 함께 제거                      |
| source          | 소스 압축 파일 다운로드                             |
| build-dep       | 소스 패키지의 빌드 의존성 설정                      |
| dist-upgrade    | 배포판 업그레이드                                   |
| dselect-upgrade | dselect 선택 따르기                                 |
| clean           | 다운로드한 압축 파일 지우기                         |
| autoclean       | 다운로드한 압축 파일 중 오래된 것 지우기            |
| check           | 의존성이 깨진 패키지를 확인합니다                   |
| changelog       | 주어진 패키지의 바꿘 내용 목록을 다운로드한 후 표시 |
| download        | 현재 디렉터리로 바이너리 패키지 다운로드            |













