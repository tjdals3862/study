# Service

##### 파드 추상화 = 파드들의 단일 엔드 포인트 + 로드밸런싱

- Service는 Selector에 의해 선택된 파드 집합 중 임의의 파드로 트래픽을 전달한다.

```yaml
apiVersion: v1
kind: Service
metadata:
	name: order
	namespace: snackbar
	labels:
	 app: order
	spec:
	 selector:
		app: order 		# 유입된 트래픽을 전달할 파드 집합
	 ports:
	 - port: 80 		# 노출할 서비스 포트
	   targetPort: 8080 # 서비스 포트와 연결할 컨테이너 포트, containerPort와 일치해야함
```





##### Endpoints: Service가 노출하는 Pod IP와 Port의 최신목록

- Service 리소스를 생성하면 Service와 같은 이름으로 Endpoints 리소스가 생성된다
- Service에 선언한 Selector의 파드 집합이 변경될 때마다 Endpoints 목록도 업데이트 된다
- Service가 받은 트래픽을 Endpoints 중에 하나로 리다이렉트한다



##### ClusterIP 타입

```
- 기본 Service 타입, Pod IP처럼 외부에서는 접근할 수 없는 IP를 할당받는다
- 이 때 Service IP는 클러스터 내부 통신용으로 사용된다
```

##### Service ClusterIP 특징

- Service는 파드 집합에 대한 단일 엔드포인트 생성한다
- Service를 생성하면 ClusterIP가 할당된다
- ClusterIP는 클러스터 내부에서만 접속 할 수 있다



##### NodePort 타입

```
- 외부에서 접근할 수 있는 External IP가 아니라 NodePort를 할당 받는다
- 할당받은 노드 Port를 통해 들어온 트래픽을 파드 집합으로 포워딩한다
```

##### Service NodePort 특징

- 클러스터 내 모든 노드에 포트 할당은 Service를 NodePort 타입으로 생성 했을 때 일어난다
- 노드의 External IP와 서비스 NodePort를 이용해서 파드에 접근 할 수 있다
- 서비스 ClusterIP도 여전히 클러스터 내부에서 사용할 수 있다



##### LoadBalancer 타입

```
- 클라우드 서비스의 Load Balancer를 프로비저닝하고 External IP를 할당 받는다
- 클라이언트는 Load Balancer IP를 통해 특정 서비스로 외부 트래픽을 포워딩할 수 있다
```

##### Service LoadBalancer 특징

- LoadBalancer 타입의 서비스를 생성하면 클라우드 서비스의 로드밸런서가 실행한다
- 로드밸런서의 IP가 Service의 External IP로 할당된다
- Service의 External IP이자 로드밸런서 IP로 외부에서 파드에 접근할 수 있다
- 서비스 ClusterIP, NodePort의 기능도 여전히 사용할 수 있다.





#### Service 관련 명령어

##### 네임스페이스 생성	

```SHELL
kubect create namespace <namespace>
```



##### 네임스페이스의 모든 리소스 조회

```
kubectl get all -n <namespace>
```



##### 네임스페이스의 Service 상세 조회

```
kubectl get svc <service-name> -o wide -n <namespace>
```



##### Service ClusterIP 조회

```
kubectl get svc <service-name> -o jsonpath="{.spec.clusterIP}" -n <namespace>
```



##### Pod 컨테이너로 명령어 전달

```
kubectl exec <pod-name> -n <namespace> -- <command>
```



##### Pod 컨테이너 환경변수 확인

```
kubectl exec <pod-name> -n <namespace> -- env | grep <pattern>
```



##### 네임스페이스에 생성한 서비스 엔드포인트 확인

```
kubectl get endpoints ‒n <namespace>
```



##### 네임스페이스에서 서비스 ClusterIP와 NodePort 확인

```
kubectl get svc <service-name> -n <namespace>
```



##### 네임스페이스에서 특정 레이블을 가진 모든 리소스 제거

```
kubectl delete all -l <label-query> -n <namespace>
```

































