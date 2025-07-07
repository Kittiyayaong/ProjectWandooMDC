# Module 7. Advanced CWPP Lab – Full Scenario

## 목표
Defender for Containers (CWPP)의 agentless scanning ➔ agent-based runtime protection ➔ VM 보호 기능(JIT, AAC, FIM)까지 end-to-end 보안 시나리오 실습

## Lab 전체 흐름
1. AKS 클러스터 배포
2. ACR 통합 + 취약 이미지 배포
3. Defender for Containers agent-based onboarding
4. Runtime protection 기능 검증

| **Step**   | **주요 작업**                                             | **목적**                                              | **Agentless / Agent-based**                                    |
| ---------- | ----------------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------- |
| **Step 1** | **AKS 클러스터 배포**                                       | Kubernetes 실습 환경(Cluster + Node Pool) 구축            | ⚫ **Prerequisite** (Agentless / Agent-based 공통 준비 단계)          |
| **Step 2** | **ACR 통합 + DVWA 취약 이미지 배포**                           | 취약 이미지(DVWA) 배포 ➔ Defender에서 이미지 취약점 평가             | 🔵 **Agentless 기능** <br>Container image vulnerability scanning |
| **Step 3** | **Defender for Containers Enable + agent onboarding** | runtime protection agent 배포 ➔ Pod/Node의 행동 기반 위협 탐지 | 🔴 **Agent-based 기능** <br>runtime protection, threat detection |
| **Step 4** | **Runtime protection 기능 검증**                          | runtime protection alert 탐지 실습                      | 🔴 **Agent-based 기능** <br>실행중 컨테이너 이상행위 탐지                     |


--- 

## Lab 진행 

### Step 1. AKS 클러스터 배포(Windows/mac 동일) 
**목표:** AKS(AKS = Azure Kubernetes Service) 클러스터 구축 및 실습 환경 준비

> ⭐ Tips. AKS (Azure Kubernetes Service)
>
> Azure에서 제공하는 Kubernetes 관리형 서비스 ➔ Kubernetes 클러스터를 Azure가 대신 설치/유지보수 해줌
> 앱을 배포, 스케일업/다운, 롤링업데이트 등 자동화 가능

< GUI > 
* AKS 클러스터 생성
→ Azure Portal ➔ Kubernetes services ➔ Create ➔ Cluster 생성 wizard

  <img width="1438" alt="image" src="https://github.com/user-attachments/assets/348191f7-3181-4318-9977-4eeb8e25e627" />

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
> * Azure에서의 namespace = Resource Provider = 클러스터 안에서 리소스를 논리적으로 구분하는 공간
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

* AKS 클러스터 인증 구성: Azure AKS 클러스터와 로컬 kubectl(PC의 Kubernetes CLI)을 연결하는 과정으로, Azure에서 클러스터 인증 정보(Kubeconfig)를 가져와서 PC의 ~/.kube/config 파일에 등록 (PC(kubectl)에서 Azure의 AKS 클러스터에 명령어를 직접 넣을 수 있도록 연결하는 과정)
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

### Step 2. ACR(Azure Container Registry)통합 + 취약 이미지 배포 -- AKS가 ACR에 있는 이미지에 접근할 수 있도록 권한을 부여하는 것
**목표:** ACR에서 취약 이미지를 pull하여 AKS에 배포

< GUI > 
* 컨테이너 배포(간단한 경우)
→ 클러스터 ➔ Workloads ➔ Deployments ➔ + create > apply a YAML (하단에 이미지 정보 기입) 

< CLI >

* Container 로그인 (Mac의 경우 Docker Desktop 앱이 실행되고 있어야 함)
```bash
# ACR login
az acr login --name <YourContainerRegistryName>
```

* imagePullSecret 생성: 쿠버네티스가 ACR에서 이미지를 가져올 때 사용할 인증 정보 저장소로, AKS가 ACR에서 이미지를 pull 할 때 이 시크릿을 사용해서 인증
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

> ⭐ Tips. 이미지 설명
> Azure에 저장해둔 DVWA 웹앱을 Kubernetes에 배포 + 공개해서, 브라우저에서 DVWA를 열고 해킹 실습을 할 수 있게 해주는 설정 파일이다.
> DVWA: “Damn Vulnerable Web Application” = 의도적으로 취약하게 만들어진 PHP/MySQL 기반 웹앱으로 웹 해킹, 취약점 학습, 보안 실습용 표준 훈련 플랫폼

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

* 배포 상태 확인 (Pod: Kubernetes에서 가장 작은 배포 단위)
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
   
> ⭐ Tips. Onboarding 방법
> * Azure Policy 자동 배포 ➔ 자동으로 DaemonSet 배포
> * 수동 Helm install ➔ 직접 DaemonSet 배포

* 배포 확인
```bash
kubectl get daemonset -A | grep azure-defender
```

> ⭐ Tips. 값 출력이 안되는경우는, portal에서 defender for container을 **ON**으로 변경했어도 설치가 안된 것으로 ➔ Helm Chart로 수동 설치 필요
>
> * AKS (Managed) 클러스터: Defender Plan ➔ ON ➔ 자동 설치 시도
> * Arc-enabled (On-prem / 다른 클라우드) 클러스터: Defender Plan ➔ ON ➔ 자동 설치 안되며, 무조건 Helm Chart 수동 설치 필요

* 정책 자동 배포 상태 확인 및 remediation
1. Azure Portal ➔ Kubernetes services ➔ 클러스터 선택 > setting ➔ Policies > [Enable add-on] 클릭 ➔ AKS 클러스터에 Azure Policy Add-on이 설치됨 (5~10분 정도 대기 (배포 완료될 때까지))
2. 배포 확인 (DaemonSet 이름에 `azure-defender` 가 포함된 리소스가 보여야 함 -- 예) `azure-defender-ds`)
```bash
kubectl get daemonset -A | grep azure
kubectl get pods -A | grep azure
```
3. defender 관련 견과값이 나오지 않기 때문에, Azure Arc 수동 onboarding 필요

* Arc onboarding: clustername 및 RG name은 azure portal에서 생성한 클러스터 정보를 통해 확인 가능  

1. Resource Provider 등록: Azure Arc + Connected K8s 사용을 위해서는 Resource Provider 등록이 선행되어야 합니다.
```bash
az provider register --namespace Microsoft.Kubernetes
az provider register --namespace Microsoft.KubernetesConfiguration
az provider register --namespace Microsoft.ExtendedLocation
az provider register --namespace Microsoft.ResourceConnector
```

2. 등록 완료 확인: 출력이 Registered여야 진행 가능
```bash
az provider show --namespace Microsoft.Kubernetes --query "registrationState"
```

3. Arc 연결 (최대 20분 소요 - Lab 클러스터(Standard_B2s)처럼 리소스가 낮으면 설치 속도 느림)
```bash
az connectedk8s connect \
  --name <ClusterName> \
  --resource-group <ResourceGroupName>
```

4. 설치 확인
```bash
kubectl get daemonset -A | grep defender
kubectl get pods -A | grep defender
```

### 결과
✅ agent-based protection 활성화 완료

> ⭐ Tips. 
> 배포하려는 Pod를 수용할 메모리가 부족해서 스케줄러가 어떤 노드에도 배치불가하여 실질적으로 trial 계정 기반의 랩에서는 사용 불가
> 차후에 용량 업그레이드 (node-vm-size Standard_B4ms) 혹은, 메모리 충분한 새 nodepool 생성 후 Pod 배포시에 제공 

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

* 프로세스 목록 확인 후 Linux 시스템 사용자 정보가 저장된 파일을 출력 ➔ 공격자가 사용자 계정 구조, 기본 권한, 잠재적 취약 계정 확인 가능    
```bash
ps aux
cat /etc/passwd
```

* 완료후에는 terminal에서 **exit**로 Root 종료

### 결과
✅ runtime protection alert 확인 
  
* MDC ➔ Alerts에서 탐지 여부 확인
  * MDC > General > Security Alert 에서 확인 
    


