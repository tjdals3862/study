# Associate Cloud Engineer

- 클라우드 솔루션 환경 설정
- 클라우드 솔루션의 성공적인 운영 보장
- 클라우드 솔루션 계획 및 구성
- 액세스 및 보안 구성
- 클라우드 솔루션 배포 및 구현



### 1. 클라우드 솔루션 환경 설정



- ##### 1.1 클라우드 프로젝트 및 계정 설정. 활동에는 다음이 포함됩니다.

- - 프로젝트 생성
  - 프로젝트 내에서 사전 정의 된 IAM 역할에 사용자 할당
  - 클라우드 ID에서 사용자 관리 (수동 및 자동화)
  - 프로젝트 내에서 API 활성화
  - 하나 이상의 Stackdriver 작업 공간 프로비저닝

- ##### 1.2 결제 구성 관리. 활동에는 다음이 포함됩니다.

- - 하나 이상의 결제 계정 만들기
  - 결제 계정에 프로젝트 연결
  - 청구 예산 및 알림 설정
  - 일일 / 월간 요금을 추정하기위한 결제 내보내기 설정

- ##### 1.3 명령 줄 인터페이스 (CLI), 특히 Cloud SDK 설치 및 구성 (예 : 기본 프로젝트 설정)

- 

### 2. 클라우드 솔루션 계획 및 구성

- 

- ##### 2.1 가격 계산기를 사용하여 GCP 제품 사용 계획 및 추정

- 

- ##### 2.2 컴퓨팅 리소스 계획 및 구성. 고려 사항은 다음과 같습니다.

- - 주어진 워크로드에 적합한 컴퓨팅 선택 (예 : Compute Engine, Google Kubernetes Engine, App Engine, Cloud Run, Cloud Functions)
  - 선점 형 VM 및 커스텀 머신 유형을 적절하게 사용

- 

- ##### 2.3 데이터 저장소 옵션 계획 및 구성. 고려 사항은 다음과 같습니다.

- - 제품 선택 (예 : Cloud SQL, BigQuery, Cloud Spanner, Cloud Bigtable)
  - 스토리지 옵션 선택 (예 : Standard, Nearline, Coldline, Archive)

- 

- ##### 2.4 네트워크 리소스 계획 및 구성. 작업에는 다음이 포함됩니다.

- - 부하 분산 옵션 차별화
  - 가용성을 위해 네트워크에서 리소스 위치 식별
  - 클라우드 DNS 구성

- 

### 3. 클라우드 솔루션 배포 및 구현



- ##### 3.1 Compute Engine 리소스 배포 및 구현. 작업에는 다음이 포함됩니다.

- - Cloud Console 및 Cloud SDK (gcloud)를 사용하여 컴퓨팅 인스턴스 시작 (예 : 디스크 할당, 가용성 정책, SSH 키)
  - 인스턴스 템플릿을 사용하여 자동 확장 된 관리 형 인스턴스 그룹 만들기
  - 인스턴스 용 커스텀 SSH 키 생성 / 업로드
  - Stackdriver 모니터링 및 로깅을위한 VM 구성
  - 컴퓨팅 할당량 평가 및 증가 요청
  - 모니터링 및 로깅을위한 Stackdriver 에이전트 설치

- 

- ##### 3.2 Google Kubernetes Engine 리소스 배포 및 구현. 작업에는 다음이 포함됩니다.

- - Google Kubernetes Engine 클러스터 배포
  - 포드를 사용하여 Google Kubernetes Engine에 컨테이너 애플리케이션 배포
  - Google Kubernetes Engine 애플리케이션 모니터링 및 로깅 구성

- 

- ##### 3.3 App Engine, Cloud Run, Cloud Functions 리소스 배포 및 구현. 해당되는 경우 작업에는 다음이 포함됩니다.

- - 애플리케이션 배포, 확장 구성, 버전 및 트래픽 분할 업데이트
  - Google Cloud 이벤트 (예 : Cloud Pub / Sub 이벤트, Cloud Storage 객체 변경 알림 이벤트)를 수신하는 애플리케이션 배포

- 

- ##### 3.4 데이터 솔루션 배포 및 구현. 작업에는 다음이 포함됩니다.

- - 제품으로 데이터 시스템 초기화 (예 : Cloud SQL, Cloud Datastore, BigQuery, Cloud Spanner, Cloud Pub / Sub, Cloud Bigtable, Cloud Dataproc, Cloud Dataflow, Cloud Storage)
  - 데이터로드 (예 : 명령 줄 업로드, API 전송, 가져 오기 / 내보내기, Cloud Storage에서 데이터로드, Cloud Pub / Sub로 데이터 스트리밍)

- 

- ##### 3.5 네트워킹 리소스 배포 및 구현. 작업에는 다음이 포함됩니다.

- - 서브넷이있는 VPC 생성 (예 : 사용자 지정 모드 VPC, 공유 VPC)
  - 커스텀 네트워크 구성 (예 : 내부 전용 IP 주소, Google 비공개 액세스, 정적 외부 및 비공개 IP 주소, 네트워크 태그)으로 Compute Engine 인스턴스 시작
  - VPC에 대한 수신 및 송신 방화벽 규칙 만들기 (예 : IP 서브넷, 태그, 서비스 계정)
  - Cloud VPN을 사용하여 Google VPC와 외부 네트워크 사이에 VPN 만들기
  - 애플리케이션 네트워크 트래픽을 애플리케이션에 배포하기위한 부하 분산기 만들기 (예 : 전역 HTTP (S) 부하 분산기, 전역 SSL 프록시 부하 분산기, 전역 TCP 프록시 부하 분산기, 지역 네트워크 부하 분산기, 지역 내부 부하 분산기)

- 

- ##### 3.6 Cloud Marketplace를 사용하여 솔루션 배포. 작업에는 다음이 포함됩니다.

- - Cloud Marketplace 카탈로그 찾아보기 및 솔루션 세부 정보보기
  - Cloud Marketplace 솔루션 배포

- 

- ##### 3.7 Cloud Deployment Manager를 사용하여 애플리케이션 인프라 배포. 작업에는 다음이 포함됩니다.

- - Deployment Manager 템플릿 개발
  - Deployment Manager 템플릿 시작

- 

### 4. 클라우드 솔루션의 성공적인 운영 보장

- 

- ##### 4.1 Compute Engine 리소스 관리. 작업에는 다음이 포함됩니다.

- - 단일 VM 인스턴스 관리 (예 : 구성 시작, 중지, 수정, 인스턴스 삭제)
  - 인스턴스에 대한 SSH / RDP
  - 새 인스턴스에 GPU 연결 및 CUDA 라이브러리 설치
  - 현재 실행중인 VM 인벤토리보기 (인스턴스 ID, 세부 정보)
  - 스냅 샷 작업 (예 : VM에서 스냅 샷 생성, 스냅 샷보기, 스냅 샷 삭제)
  - 이미지 작업 (예 : VM 또는 스냅 샷에서 이미지 만들기, 이미지보기, 이미지 삭제)
  - 인스턴스 그룹 작업 (예 : 자동 확장 매개 변수 설정, 인스턴스 템플릿 할당, 인스턴스 템플릿 생성, 인스턴스 그룹 삭제)
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, GCloud SDK)

- 

- ##### 4.2 Google Kubernetes Engine 리소스 관리. 작업에는 다음이 포함됩니다.

- - 현재 실행중인 클러스터 인벤토리 (노드, 포드, 서비스)보기
  - 컨테이너 이미지 저장소 찾아보기 및 컨테이너 이미지 세부 정보보기
  - 노드 풀 작업 (예 : 노드 풀 추가, 수정, 삭제)
  - 창 작업 (예 : 창 추가, 편집 또는 제거)
  - 서비스 작업 (예 : 서비스 추가, 편집 또는 제거)
  - 상태 저장 응용 프로그램 작업 (예 : 영구 볼륨, 상태 저장 세트)
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, Cloud SDK)

- 

- ##### 4.3 App Engine 및 Cloud Run 리소스 관리. 작업에는 다음이 포함됩니다.

- - 애플리케이션 트래픽 분할 매개 변수 조정
  - 자동 확장 인스턴스에 대한 확장 매개 변수 설정
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, Cloud SDK)

- 

- ##### 4.4 스토리지 및 데이터베이스 솔루션 관리. 작업에는 다음이 포함됩니다.

- - Cloud Storage 버킷간에 객체 이동
  - 저장소 등급간에 Cloud Storage 버킷 변환
  - Cloud Storage 버킷에 대한 객체 수명주기 관리 정책 설정
  - 쿼리를 실행하여 데이터 인스턴스 (예 : Cloud SQL, BigQuery, Cloud Spanner, Cloud Datastore, Cloud Bigtable)에서 데이터 검색
  - BigQuery 쿼리 비용 추정
  - 데이터 인스턴스 (예 : Cloud SQL, Cloud Datastore) 백업 및 복원
  - Cloud Dataproc, Cloud Dataflow 또는 BigQuery에서 작업 상태 검토
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, Cloud SDK)

- 

- ##### 4.5 네트워킹 리소스 관리. 작업에는 다음이 포함됩니다.

- - 기존 VPC에 서브넷 추가
  - 더 많은 IP 주소를 갖도록 서브넷 확장
  - 고정 외부 또는 내부 IP 주소 예약
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, Cloud SDK)

- 

- ##### 4.6 모니터링 및 로깅. 작업에는 다음이 포함됩니다.

- - 리소스 측정 항목을 기반으로 Stackdriver 알림 만들기
  - Stackdriver 커스텀 측정 항목 만들기
  - 로그를 외부 시스템 (예 : 온 프레미스 또는 BigQuery)으로 내보내도록 로그 싱크 구성
  - Stackdriver에서 로그보기 및 필터링
  - Stackdriver에서 특정 로그 메시지 세부 정보보기
  - 클라우드 진단을 사용하여 애플리케이션 문제 조사 (예 : Cloud Trace 데이터보기, Cloud Debug를 사용하여 애플리케이션 시점보기)
  - Google Cloud Platform 상태보기
  - 관리 인터페이스 작업 (예 : Cloud Console, Cloud Shell, Cloud SDK)

- 

### 5. 액세스 및 보안 구성



- ##### 5.1 ID 및 액세스 관리 (IAM) 관리. 작업에는 다음이 포함됩니다.

- - IAM 역할 할당보기
  - 계정 또는 Google 그룹에 IAM 역할 할당
  - 사용자 지정 IAM 역할 정의

- 

- ##### 5.2 서비스 계정 관리. 작업에는 다음이 포함됩니다.

- - 제한된 권한으로 서비스 계정 관리
  - VM 인스턴스에 서비스 계정 할당
  - 다른 프로젝트의 서비스 계정에 대한 액세스 권한 부여

- 5.3 프로젝트 및 관리 서비스에 대한 감사 로그보기.