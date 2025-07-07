# Module 7. (for MAC) Advanced CWPP Lab – Full Scenario

## 목표
Defender for Containers (CWPP)의 agentless scanning ➔ agent-based runtime protection ➔ VM 보호 기능(JIT, AAC, FIM)까지 end-to-end 보안 시나리오 실습

## Lab 전체 흐름
1. AKS 클러스터 배포
2. ACR 통합 + 취약 이미지 배포
3. Defender for Containers agent-based onboarding
4. Runtime protection 기능 검증
5. Admission control policy 구성
6. JIT / AAC / FIM 설정 (노드풀 VM)
7. Alert & Recommendation 분석

| **Step**   | **주요 작업**                                         | **목적**                                              | **Agentless / Agent-based**                                  |
| ---------- | ------------------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------ |
| **Step 1** | AKS 클러스터 배포                                       | Kubernetes 환경 구축 (실습 인프라 준비)                        | ⚫ 준비 단계 (Agentless/Agent-based 모두 prerequisite)              |
| **Step 2** | ACR 통합 + DVWA 취약 이미지 배포                           | 취약한 컨테이너 이미지 배포 ➔ Defender가 이미지 취약점 평가 가능           | 🔵 **Agentless 기능** (Container image vulnerability scanning) |
| **Step 3** | Defender for Containers Enable + agent onboarding | runtime protection agent 배포 ➔ Pod/Node의 행동 기반 위협 탐지 | 🔴 **Agent-based 기능** (runtime protection, threat detection) |


--- 

## Lab 진행 

### Step 1. AKS 클러스터 배포(Windows/mac 동일) 
**목표:** AKS(AKS = Azure Kubernetes Service) 클러스터 구축 및 실습 환경 준비

< GUI > 
* AKS 클러스터 생성
→ Azure Portal ➔ Kubernetes services ➔ Create ➔ Cluster 생성 wizard

< CLI >
* 리소스 그룹 생성
```bash
az group create --name CWPP-Lab-RG --location koreacentral
```

* AKS 클러스터 생성
```bash
az aks create \
  --resource-group CWPP-Lab-RG \
  --name cwppaks \
  --node-count 1 \
  --enable-addons monitoring \
  --generate-ssh-keys \
  --node-vm-size Standard_B2s
```

> ⭐ Tips. Namespace란?
>
> * Azure에서의 namespace = Resource Provider
> * 기본적으로 비활성화(unregistered)상태이기 때문에, 사용전에 register 명령으로 사용 가능하도록 등록
> 
|                       |                                                              |
| --------------------- | ------------------------------------------------------------ |
| **Resource Provider** | Azure에서 특정 **서비스나 리소스를 관리하는 논리 단위**                          |
| **Namespace**         | Resource Provider의 고유 이름 <br>(예: Microsoft.ContainerService) |
| **역할**                | Subscription이 해당 서비스를 사용할 수 있도록 **권한을 등록**하는 개념              |

* 등록 필요한 namespace list
  
| 작업                                                               | 의미                                                         |
| ---------------------------------------------------------------- | ---------------------------------------------------------- |
| `az provider register --namespace Microsoft.ContainerService`    | 내 Subscription에서 **AKS (Kubernetes Service)를 쓸 수 있게 등록** |
| `az provider register --namespace Microsoft.Insights`            | **Monitoring, Metrics 기능**을 쓸 수 있게 등록                    |
| `az provider register --namespace Microsoft.OperationalInsights` | **Log Analytics Workspace 기능**을 쓸 수 있게 등록                |

* 등록 완료 후 **registered**라고 올라와야함.
```bash
az provider show --namespace Microsoft.ContainerService --query "registrationState"
az provider show --namespace Microsoft.Insights --query "registrationState"
az provider show --namespace Microsoft.OperationalInsights --query "registrationState"
```

* AKS 클러스터 인증 구성
```bash
az aks get-credentials --resource-group CWPP-Lab-RG --name cwppaks
```
 
* 노드 풀 확인
```bash
kubectl get nodes
```

### 결과
✅ AKS 클러스터 생성 완료

---

### Step 2. ACR 통합 + 취약 이미지 배포
**목표:** ACR에서 취약 이미지를 pull하여 AKS에 배포

< GUI > 
* 컨테이너 배포(간단한 경우)
→ 클러스터 ➔ Workloads ➔ Deploy ➔ YAML 입력 또는 Quick deployment

< CLI >
* Container 로그인 (Mac의 경우 Docker Desktop 앱이 실행되고 있어야 함)
```bash
# ACR login
az acr login --name <YourContainerRegistryName>
```
* imagePullSecret 생성
```bash
kubectl create secret docker-registry acr-secret \
  --docker-server=<YourContainerRegistryName>.azurecr.io \
  --docker-username=<ACR_USERNAME> \
  --docker-password=<ACR_PASSWORD>
```
> ⭐ Tips. username과 Password는 ACR Admin 계정 사용
>
> 1. Azure Portal ➔ Container Registry ➔ Settings > Access keys
> 2. Admin user 를 ON
> 3. 아래 정보 확인:
>
| 항목                       | 의미               |
| ------------------------ | ---------------- |
| **Username**             | `<ACR_USERNAME>` |
| **Password / Password2** | `<ACR_PASSWORD>` |


* DVWA deployment manifest 작성 후 저장 (dvwa-deployment.yaml) -- `VSCode`에서 진행 (없으면 다운로드)하며 데스크탑에 저장 후 과정 진행 -- DVWA 이미지를 명시한 yaml 파일을 kubectl apply로 배포
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dvwa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dvwa
  template:
    metadata:
      labels:
        app: dvwa
    spec:
      containers:
      - name: dvwa
        image: <YourContainerRegistryName>.azurecr.io/vulnerables/web-dvwa
      imagePullSecrets:
      - name: acr-secret
---
apiVersion: v1
kind: Service
metadata:
  name: dvwa
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: dvwa
```
* 터미널에서 저장위치(본 랩에서는 데스크탑)로 이동 
```bash
cd ~/Desktop
```

* 배포
```bash
kubectl apply -f dvwa-deployment.yaml
```

* 배포 상태 확인
```bash
kubectl get pods
kubectl get svc
```

### 결과
✅ DVWA pod 실행 확인
```bash
kubectl get pods
```

✅ 위 <pod-name>에는 kubectl get pods 명령어에서 나온 pod 이름을 복사해서 사용
```bash
kubectl describe pod <pod-name>
```
---

### Step 3. Defender for Containers agent-based onboarding
**목표:** runtime protection 기능 활성화

* Portal에서 defender for container **On**
1. MDC ➔ Environment settings ➔ Subscription ➔ Defender Plans ➔ **Defender for Containers Enable**
2. Onboarding 방법 선택:
   - Azure Policy 자동 배포
   - 수동 Helm install (선택 시 아래 실행) -- Azure Policy를 통해 자동으로 에이전트 배포하는 대신, 직접 Helm Chart를 내려받아 수동으로 설치하는 방법.

* 정책 자동 배포 상태 확인 및 remediation
1. Azure Portal ➔ Kubernetes services ➔ 클러스터 선택 > setting ➔ Policies > [Enable add-on] 클릭 ➔ AKS 클러스터에 Azure Policy Add-on이 설치됨 (5~10분 정도 대기 (배포 완료될 때까지))
2. 배포 확인
```bash
kubectl get daemonset -A | grep azure
kubectl get pods -A | grep azure
```

### 결과
✅ agent-based protection 활성화 완료

> ⭐ Tips. 
>
> Agentless는 클라우드 메타데이터를 통해 분석, Agent-based는 노드 내부 runtime activity를 탐지하므로 둘 다 구성해야 완전한 Defender for Containers 기능을 사용
> 
> 사용 이유
> * 이미지 스캔, 취약점 진단 ➔ 배포 전에만 보안 검증 가능
> * 배포 후에는 새로운 취약점이 나올 수도 있고, 컨테이너 내부에서 공격자가 명령을 실행할 수도 있음
>
> Runtime Protection 역할
> * 컨테이너가 실행 중일 때: 누군가가 이상한 프로세스를 실행한다거나, 의심스러운 네트워크 통신을 시도한다거나, 비정상적인 시스템 호출이 발생할 때
> * 실시간으로 탐지하고 Alert를 생성함

---

### Step 4. Runtime protection 기능 검증
**목표:** 실행 중인 컨테이너 보호 기능 확인

> ⭐ Tips. Runtime Protection 기능이란?
>
> * 컨테이너가 실행되는 중(runtime) 에 일어나는 이상 행위, 악성 행위, 취약점 악용 행위를 탐지하고 보호하는 기능

| **Pod**            | **용도**                                                                |
| ------------------ | --------------------------------------------------------------------- |
| **DVWA pod**       | 취약 이미지 배포 ➔ Defender agentless 스캔 실습                                  |
| **test-nginx pod** | curl 등 suspicious command 실행 ➔ runtime protection(alert detection) 실습 |

< test-nginx pod에서 실행 >
* test-nginx pod 생성
```bash
kubectl run test-nginx --image=nginx --restart=Never --command -- sleep 3600
```

* Pod 상태 확인
```bash
kubectl get pods
```

> ⭐ Tips.  pod 상태가 Pending / CrashLoopBackOff 라면 ➔ 이벤트 확인
> ```bash
> kubectl describe pod test-nginx
> ```

* Pod로 진입
```bash
kubectl exec -it test-ubuntu -- /bin/bash
```
  
* suspicious process 실행 예시
  * /etc/passwd 출력 = 정보수집 공격
  * 패스워드 유출을 통해  ➔ 공격자가 시스템 사용자 정보를 얻어 후속 공격(권한 상승, lateral movement) 기반으로 사용
  * Defender for Containers의 Runtime protection 기능에서, suspicious process 실행을 탐지 ➔ Alert 발생 ➔ 대응 조치
    
```bash
ps aux
cat /etc/passwd
```

* 완료후에는 terminal에서 **exit**로 Root 종료

### 결과
✅ runtime protection alert 확인 
  
* MDC ➔ Alerts에서 탐지 여부 확인
  * MDC > General > Security Alert 에서 확인 
    
---

### Step 5. Admission control policy 구성
**목표:** 취약 이미지 배포 차단

### 작업
1. MDC ➔ Defender for Containers ➔ Admission control policy ➔ **Enable**
2. Policy: High severity vulnerability 이미지 배포 차단
3. DVWA 취약 이미지 redeploy 시도 ➔ 배포 실패 확인

```bash
kubectl delete -f dvwa-deployment.yaml
kubectl apply -f dvwa-deployment.yaml
```

### 결과
✅ admission controller 차단 기능 검증

---

### Step 6. JIT / AAC / FIM 설정 (노드풀 VM)
**목표:** CWPP VM 보호 기능 실습

### 작업
#### 🔹 JIT
1. MDC ➔ Just-In-Time VM Access ➔ Node pool VM ➔ JIT 구성
2. SSH 포트 요청 ➔ 승인 ➔ 접속 확인

#### 🔹 AAC
1. MDC ➔ Adaptive Application Controls ➔ Node pool VM ➔ 정책 적용
2. 승인되지 않은 binary 실행 ➔ 차단 여부 확인

#### 🔹 FIM
1. MDC ➔ File Integrity Monitoring ➔ Node pool VM ➔ 보호 경로 파일 변경 ➔ alert 발생 여부 확인

### 결과
✅ VM 보호 기능 실습 완료

---

### Step 7. Alert & Recommendation 분석
**목표:** 탐지된 alert 및 remediation recommendation 분석

### 작업
1. MDC ➔ Alerts ➔ Container & VM 탐지 내용 검토
2. MDC ➔ Recommendations ➔ remediation guidance 확인

### 결과
✅ CWPP 탐지 및 대응 워크플로우 이해


