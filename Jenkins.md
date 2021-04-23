# Jenkins

## 1. Jenkins ?

- Jenkins는 Java로 제작된 오픈소스 **지속적 통합(CI, Continuous Integration) 도구**
- Jenkins에는 Tomcat 서버가 내장되어 **Servlet Container 위에 돌아가는 웹 서버**
- 쉽게 빌드 결과물을 만들고 테스트하며 배포할 수 있는 유용한 도구

## 2. Jenkins 시작하기

### 2.1 Jenkins 다운로드 및 설치

#### 2.1.1 Window

- [다운로드](https://jenkins.io/download/thank-you-downloading-windows-installer-stable/)
- 정상적으로 설치가 완료되면 Jenkins 웹 서버가 자동으로 구동(`localhost:8080`)

#### 2.1.2 Ubuntu

- Jenkins는 java가 필요하므로, java가 설치되어 있는지 확인 아니면 설치

  ```bash
  # 설치 확인
  $ java -version
  
  # 설치
  $ sudo apt-get install openjdk-8-jdk
  ```

- Jenkins 설치를 위한 repository key 추가

  ```bash
  $ wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
  ```

- repository 추가

  ```bash
  $ echo deb https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list
  ```

- apt-get 업데이트 후 jenkins 설치

  ```bash
  $ sudo apt-get update
  $ sudo apt-get install jenkins
  ```

- Jenkins 실행 전 포트 변경

  ```bash
  $ sudo vi /etc/default/jenkins 
  ```

  - 파일 안에서 HTTP_PORT를 찾아 원하는 포트로 변경

    ```
    # port for HTTP connector (default 8080; disable with -1)
    HTTP_PORT=<포트 번호>
    ```

- jenkins 실행

  ```bash
  # jenkins 자동 실행
  $ sudo systemctl enable jenkins
  
  # jenkins 실행 상태 확인
  $ sudo systemctl status jenkins
  
  # jenkins 실행
  $ sudo systemctl start jenkins
  ```

### 2.2 잠금 해제

- 관리자 암호를 입력하라는 페이지가 나오면

  ![img](Jenkins(Windows).assets/99DB403C5C5CDC6709.png)

- `C:\Program Files (x86)\Jenkins\secrets`에서 `initialAdminPassword`에서 비밀번호를 읽어 입력

  ![image-20200311160334870](Jenkins(Windows).assets/image-20200311160334870.png)

### 2.3 설치 진행

- 입력 후 `Install suggested plugins` 선택

  ![img](Jenkins(Windows).assets/9995B4335C5CDCE905.png)

### 2.4 관리자 계정 설정 및 마무리

![image-20200311160808276](Jenkins(Windows).assets/image-20200311160808276.png)

- 세팅 완료

  ![image-20200311160925304](Jenkins(Windows).assets/image-20200311160925304.png)

- `localhost:8080`으로 접속하면

  ![image-20200311161055072](Jenkins(Windows).assets/image-20200311161055072.png)

- 포트 번호를 바꿔주고 싶다면 `C:\Program Files (x86)\Jenkins\jenkins.xml`에서 `httpPort=` 수정

  ![image-20200311161331777](Jenkins(Windows).assets/image-20200311161331777.png)

### 3. 설정

- Jenkins 메인 페이지에서 **Jenkins 관리**를 누르고, **Global Tool Configuration** 메뉴 진입

![image-20200311162620756](Jenkins(Windows).assets/image-20200311162620756.png)

### 3.1 Maven 설정

- maven이 설치되어 있지 않다면 [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)에서 다운로드
- 압축을 풀고 시스템 환경변수 `path`에 `[Maven 경로]/bin`을 등록

- **Settings file in filesystem**과 **Global settings file on filesystem**을 선택 후<br> `maven 경로/conf/settings.xml`을 등록

  ![image-20200311163559236](Jenkins(Windows).assets/image-20200311163559236.png)

- 밑으로 내리면 **Maven 메뉴**가 보이는데 **Add Maven** 버튼을 누르고 `install automatically` 체크 해제

- **MAVEN_HOME**에 경로 입력

  ![image-20200311163844676](Jenkins(Windows).assets/image-20200311163844676.png)

### 3.2 JDK

- **Add JDK** 버튼을 누르고 `install automatically` 체크 해제

- Maven과 마찬가지로 **JAVA_HOME**에 jdk  경로 입력

  ![image-20200311165108325](Jenkins(Windows).assets/image-20200311165108325.png)

### 3.3 GIT

- **GIT**에서 경로를 지정 없다면 [다운로드](https://git-scm.com/downloads)

![image-20200311165312053](Jenkins(Windows).assets/image-20200311165312053.png)

### 3.4 기타 관리

![image-20200311165655479](Jenkins(Windows).assets/image-20200311165655479.png)

#### 3.4.1 Plugin 설치

- 필요한 플러그인은 다음과 같음
  - Git plugin
  - GItHub plugin (GitLab도 가능)
  - Deploy to container plugin
- 처음 설치할때 **Suggested plugin**을 선택했다면, Git과 GitHub 플러그인은 기본으로 설치되어 있음

![image-20200314161355676](Jenkins(Windows).assets/image-20200314161355676.png)

- 설치 후 재시작

#### 3.4.2 시스템 설정

- 시스템 설정 - Jenkins URL의 LocalHost를 현재 컴퓨터의 IP로 변경

  ![image-20200316102324557](Jenkins(Windows).assets/image-20200316102324557.png)

## 4. Git Setting

### 4.1 Git 토큰 발급

- **프로필**을 누르고 **Settings** 진입

- 왼쪽 사이드 메뉴에서 **Developer setting** 진입

  ![image-20200314164742550](Jenkins(Windows).assets/image-20200314164742550.png)

- 진입후 **Personal access tokens** 클릭

  ![image-20200314164853664](Jenkins(Windows).assets/image-20200314164853664.png)

- **Generate new token**을 눌러 새 토큰을 발급

  - **repo**와 **admin:repo_hook** 체크

  ![image-20200314165126863](Jenkins(Windows).assets/image-20200314165126863.png)

- **Generate token하고 발급 받은 토큰을 복사**

### 4.2 Git - Jenkins 연동

- Jenkins 관리로 돌아와서 **시스템 설정**

  ![image-20200314165438316](Jenkins(Windows).assets/image-20200314165438316.png)

- **GitHub**를 찾아서 **Add GitHub Server**를 누르고 API URL은 그대로 두고 **Add 버튼**을 클릭

  - **kind를 Secret text**, **Secret**에 아까 Git에서 발급받은 토큰과 구분용 ID를 입력

    ![image-20200314165748193](Jenkins(Windows).assets/image-20200314165748193.png)

- Test connection을 하면 정상적으로 연동이 되는지 확인 가능하다.

  ![image-20200314170042423](Jenkins(Windows).assets/image-20200314170042423.png)

## 5. GitHub 프로젝트 연동 및 자동 배포

### 5.1 GitHub 프로젝트 연동

- **Jenkins 메인페이지**에서, **New Item 메뉴**를 선택 후 **Freestyle project** 진입

  ![image-20200314170821676](Jenkins(Windows).assets/image-20200314170821676.png)

- **GitHub project 체크** 후 프로젝트 URL을 입력

  ![image-20200314171022469](Jenkins(Windows).assets/image-20200314171022469.png)

- **소스코드 관리** 탭에서 **Git을 선택 후 Repository URL**에 프로젝트 URL에 .git을 붙인 URL을 입력

  ![image-20200314171234263](Jenkins(Windows).assets/image-20200314171234263.png)

- **Credentials**에서 Add 버튼을 누르고, Git id/pw를 이용한다면 username, password에 각각 입력

  ![image-20200314171456743](Jenkins(Windows).assets/image-20200314171456743.png)

### 5.2 Webhook

- **GitHub repository - Settings - Webhooks 메뉴에서 add webhook 클릭**

- Payload URL에는 `Jenkins 주소/github-webhook/`을 입력

  ![image-20200316113437245](Jenkins(Windows).assets/image-20200316113437245.png)

- 다시 젠킨스로 돌아와서 프로젝트의 **빌드 유발** 탭에서 **GitHub hook trigger for GITScm polling** 체크

  ![image-20200316114059278](Jenkins(Windows).assets/image-20200316114059278.png)

- Build 탭에서 **Invoke top-level Maven targets** 선택 후 아래와 같이 입력

  ![image-20200316114312172](Jenkins(Windows).assets/image-20200316114312172.png)

### 5.3 자동 배포

- **빌드 후 조치** 탭에서 **Deploy war/ear a container**를 선택 후

- 다음과 같이 입력

  ![image-20200314174922852](Jenkins(Windows).assets/image-20200314174922852.png)

- 배포 서버의 톰켓경로를 찾아서 `톰켓경로/conf/tomcat-user.xml`에래 role과 user를 추가

  ```xml
  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-status"/>
  <user name="아이디" password="패스워드" roles="manager-gui,manager-script,manager-status" />
  ```

- tomcat URL과 Credentials를 입력

  ![image-20200314175836325](Jenkins(Windows).assets/image-20200314175836325.png)

- 만약 아파치 톰켓이 설치된 `설치루트/webapps`에 **manager 폴더**가 없다면 홈페이지에서 압축파일을 받아서 가져오자

- 또한 `localhost:포트/manager`에서 **403 애러**가 난다면 `/webapps/manager/META-INF`의 `context.xml` 수정

  ```xml
  <!--
  	<value ... />
  -->
  ```

- Jenkins로 돌아와서 **Build Now**

  ![image-20200317123627363](Jenkins(Windows).assets/image-20200317123627363.png)

- 빌드 성공 여부

  ![image-20200317123651323](Jenkins(Windows).assets/image-20200317123651323.png)

- 주소로 들어가 보면 확인

  ![image-20200317123824543](Jenkins(Windows).assets/image-20200317123824543.png)

